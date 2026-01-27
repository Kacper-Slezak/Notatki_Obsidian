# Raport z Testów Systemu Kontroli Dostępu FaceOn

**Zespół:** Kacper Ślęzak, Gabriela Solich, Martyna Peukert 1

**Status Systemu:** Zweryfikowany pozytywnie

## 1. Wstęp

Niniejszy raport dokumentuje proces weryfikacji systemu weryfikacji dwuskładnikowej (2FA), opartego na kodach QR oraz biometrii twarzy. Testy potwierdziły spełnienie wymagań funkcjonalnych i nie funkcjonalnych.

## 2. Testy Automatyczne

Użyto frameworka `pytest` z mechanizmem `unittest.mock` do izolacji procesów AI (DeepFace) oraz wysyłki e-mail.

### 2.1. Moduł Administracyjny 

Weryfikacja zarządzania bazą pracowników przez panel administracyjny4.

- **Pobieranie pracowników (`test_get_all_employees`):** Potwierdzono poprawne zwracanie listy osób przez endpoint `/admin/employees`.
    
- **Aktualizacja profilu ze zdjęciem (`test_update_employee_profile_with_photo`):** Sprawdzono mechanizm przeliczania wektorów biometrycznych przy zmianie zdjęcia.
    
- **Usuwanie pracowników:** Zweryfikowano scenariusz sukcesu (200 OK) oraz obsługę błędu 404 dla nieistniejących identyfikatorów UUID.
    

### 2.2. Moduł Terminala i Autoryzacji

Weryfikacja logiki terminala CV zgodnie z diagramem aktywności.

- **Pełny sukces (2FA):** Scenariusz, w którym kod QR jest aktywny, a twarz pasuje do wzorca (status: `GRANTED`).
    
- **Błędy Biometrii:**
    
    - **Mismatch:** Kod QR poprawny, ale twarz innej osoby (status: `DENIED`, reason: `FACE_MISMATCH`).
        
    - **Brak twarzy:** Brak wykrycia twarzy w klatce (reason: `NO_FACE_DETECTED`).
        
    - **Wiele twarzy:** Wykrycie więcej niż jednej osoby (reason: `MULTIPLE_FACES`) - kluczowe dla bezpieczeństwa.
        
- **Weryfikacja statusu pracownika:**
    
    - **Nieaktywny:** Blokada dostępu dla osób z flagą `is_active=False`.
        
    - **Wygasły:** Blokada dostępu po dacie `expires_at`.
        

### 2.3. Weryfikacja Logowania Zdarzeń 

Zgodnie z wymaganiem niefunkcjonalnym dotyczącym audytu, system loguje każdą próbę wejścia do tabeli `AccessLog`.

- **Logowanie sukcesu:** Zapis statusu `GRANTED` i powiązanie logu z UUID pracownika.
    
- **Logowanie błędów:** System poprawnie rozróżnia i loguje przyczyny odmowy: `QR_INVALID_FORMAT`, `QR_INVALID_OR_INACTIVE` oraz `MULTIPLE_FACES`.
    

## 3. Testy Manualne 

Testy manualne przeprowadzono na sprzęcie docelowym (Laptop Vivobook S14, kamera wbudowana).

### 3.1. Wydajność (Czas Przetwarzania)

**Wymaganie:** Całkowity czas uwierzytelniania < 5 sekund.

| **Scenariusz**                                 | **Średni czas (stoper)** | **Status** | Liczba prób |
| ---------------------------------------------- | ------------------------ | ---------- | ----------- |
| Dopasowana twarz do kodu qr, dobre oświetlenie | 3.2 s                    | **PASSED** | 30          |

### 3.2. Dokładność Rozpoznawania

Wymaganie: Trafność identyfikacji min. 90%.

Model: Facenet512 (DeepFace) z progiem odległości kosinusowej 0.3.

| **Próba**               | **Liczba testów** | **Sukcesy** | **Błędy** | **Skuteczność** |
| ----------------------- | ----------------- | ----------- | --------- | --------------- |
| **Właściwy użytkownik** | 50                | 49          | 1         |  98%            |
| **Atak (podszywanie)**  | 50                | 15          | 0         | 100%            |

### 3.3 Funkcjonalność Panelu Administratora

Dodatkowo ręcznie przeprowadzono testy wszystkich funkcjonalności panelu administratora aby sprawdzić ich poprawność działania. Wszystkie testy przeszły pomyślnie.