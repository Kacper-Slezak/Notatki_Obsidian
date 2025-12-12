### 1. Przegląd Projektu

- **Nazwa Projektu:** FactoryGuard
    
- **Cel:** Zastąpienie podatnego na nadużycia systemu kart magnetycznych1. Projekt wdraża system kontroli dostępu oparty na dwuskładnikowym uwierzytelnianiu (2FA): Skan kodu QR (coś, co masz) i Weryfikacja twarzy (ktoś, kim jesteś)2.
    
- **Kluczowe Technologie:** React, Python (FastAPI, OpenCV), PostgreSQL, Docker.
    

### 2. Zespół i Role

Zgodnie z ustaleniami, role są "główne", ale oczekiwana jest ścisła współpraca i wzajemne wsparcie.

|**Członek Zespołu**|**Rola**|**Główne Obowiązki**|
|---|---|---|
|**Kacper Ślęzak**|**Team Lead** / **Backend Developer**|Zarządzanie projektem, architektura, kluczowa logika backendu, Infrastruktura (Docker), integracja systemów.|
|**Gabriela Solich**|**Backend Developer**|Projekt bazy danych, implementacja endpointów API, logika biznesowa (raporty, uprawnienia), wsparcie dla CV.|
|**Martyna Peukert**|**Frontend Developer**|Implementacja `FactoryGuard-Admin-UI` (React), UI/UX panelu, integracja z API backendowym.|

### 3. Architektura Systemu i Stos Technologiczny

System składa się z 4 głównych komponentów, zgodnie z waszym diagramem architektury3:

1. **`FactoryGuard-API-Service` (Backend)**
    
    - **Opis:** Centralne API obsługujące całą logikę biznesową.
        
    - **Technologia:** Python (FastAPI)
        
    - **Właściciele:** Kacper, Gabriela
        
2. **`PostgreSQL DB` (Baza Danych)**
    
    - **Opis:** Przechowuje dane pracowników, wektory biometryczne i logi dostępu.
        
    - **Technologia:** PostgreSQL
        
    - **Właściciele:** Gabriela (projekt), Kacper (admin)
        
3. **`FactoryGuard-Admin-UI` (Frontend)**
    
    - **Opis:** Panel dla administratora (React) do zarządzania systemem.
        
    - **Technologia:** React
        
    - **Właściciel:** Martyna
        
4. **`FactoryGuard-CV-Terminal` (Klient)**
    
    - **Opis:** Aplikacja na urządzeniu przy wejściu, obsługująca kamerę.
        
    - **Technologia:** Python (OpenCV, DeepFace)
        
    - **Właściciele:** Kacper, Gabriela
        

### 4. Kluczowe Wymagania Systemowe (Podsumowanie)

					Na podstawie dokumentacji 4444i notatek5:

#### Wymagania Funkcjonalne

- **Panel Admina:**
    
    - CRUD (Dodawanie, Odczyt, Aktualizacja, Deaktywacja) Pracowników66.
        
    - Dodawanie zdjęć/wideo jako wzorca biometrycznego77.
        
    - Zarządzanie uprawnieniami (Aktywacja/Deaktywacja pracownika)88.
        
    - Generowanie kodów QR dla pracowników (stałych, powiązanych z kontem)99.
        
    - Generowanie i przeglądanie raportów wejść (poprawnych i niepoprawnych)1010.
        
- **Terminal Dostępowy:**
    
    - Oczekiwanie na kod QR11.
        
    - Po zeskanowaniu QR, aktywacja skanu twarzy12.
        
    - Weryfikacja 1:1 (Czy twarz z kamery pasuje do wzorca z bazy powiązanego z QR?)13.
        
    - Logowanie każdej próby (udanej i nieudanej) do API14.
        

#### Wymagania Niefunkcjonalne (NFR)

- **(NFR-01) Wydajność:** Całkowity czas przetwarzania (QR + Twarz) **< 5 sekund**151515.
    
- **(NFR-02) Dokładność:** Trafność identyfikacji twarzy min. 90%161616.
    
- **(NFR-03) Przechowywanie Danych:** Raporty muszą być dostępne przez **6 miesięcy**171717.
    
- **(NFR-04) Skalowalność:** System musi obsłużyć co najmniej **20 pracowników**18.
    
- **(NFR-05) Bezpieczeństwo:** Po udanym wejściu, terminal powinien być zablokowany na **1 minutę** (zgodnie z diagramem 19).
    

---

### 5. Podział Zadań (Wstępny Work Breakdown)

Oto propozycja podziału na główne "Epiki" (duże moduły) i zadania.

#### ⚙️ Epik 1: Infrastruktura i Ustawienie Projektu

- **Właściciel:** Kacper
    
- **Zadania:**
    
    - Utworzenie repozytorium Git i ustalenie strategii branchy (np. GitFlow).
        
    - Konfiguracja `Docker Compose` dla środowiska deweloperskiego (API + Baza + Frontend).
        
    - Utworzenie "boilerplate" (pustego szkieletu) dla projektu FastAPI.
        
    - Utworzenie "boilerplate" dla projektu React (`create-react-app`).
        

#### 🗄️ Epik 2: Rdzeń Backendu i Baza Danych

- **Właściciele:** Gabriela, Kacper
    
- **Zadania:**
    
    - **[Gabi]** Projekt schematu bazy danych (Tabele: `Employees`, `AccessLogs`, `FaceEmbeddings`).
        
    - **[Gabi]** Implementacja modeli (np. SQLAlchemy) i schematów (Pydantic) dla API.
        
    - **[Kacper]** Implementacja logiki generowania wektorów biometrycznych (embeddingów) podczas dodawania pracownika.
        
    - **[Gabi]** Zabezpieczenie API (np. logowanie dla admina, klucze API dla terminala).
        

#### 🖥️ Epik 3: Panel Administracyjny (Frontend + API)

- **Właściciele:** Martyna (Frontend), Gabi (Backend API)
    
- **Zadania:**
    
    - **[Martyna]** Projekt widoków UI (Lista pracowników, Dodawanie, Raporty).
        
    - **[Gabi]** Implementacja endpointów API dla Admina:
        
        - `GET /employees` (lista)
            
        - `POST /employees` (dodawanie + upload zdjęcia)
            
        - `PUT /employees/{id}` (edycja)
            
        - `GET /access-logs` (raporty z filtrowaniem)
            
        - `GET /employees/{id}/qr-code` (generowanie QR)
            
    - **[Martyna]** Zaimplementowanie widoku "Lista Pracowników" (pobieranie i wyświetlanie).
        
    - **[Martyna]** Zaimplementowanie formularza "Dodaj Pracownika" (z wysyłaniem zdjęcia).
        
    - **[Martyna]** Zaimplementowanie widoku "Raporty".
        

#### 📷 Epik 4: Logika Terminala CV (Aplikacja + API)

- **Właściciele:** Kacper, Gabi
    
- **Zadania:**
    
    - **[Kacper]** Implementacja endpointów API dla Terminala:
        
        - `GET /employees/by-qr/{qr_uuid}` (pobranie ID pracownika i wektora twarzy)
            
        - `POST /access-logs` (zapisanie próby wejścia: GRANTED/DENIED)
            
    - **[Kacper]** Stworzenie skryptu Python (`FactoryGuard-CV-Terminal`).
        
    - **[Gabi]** Implementacja logiki odczytu kamery i detekcji QR (OpenCV).
        
    - **[Kacper]** Implementacja logiki detekcji twarzy i weryfikacji 1:1 (np. `DeepFace.verify`).
        
    - **[Kacper, Gabi]** Złożenie całości w logikę przepływu (Skan QR -> API -> Skan Twarzy -> Weryfikacja -> API Log)20.
        

#### ✅ Epik 5: Testowanie i Demo

- **Właściciele:** Wszyscy
    
- **Zadania:**
    
    - **[Wszyscy]** Testy manualne E2E (End-to-End):
        
        1. Martyna dodaje pracownika w panelu.
            
        2. Kacper/Gabi używają QR i twarzy na terminalu.
            
        3. Martyna sprawdza log w raporcie.
            
    - **[Kacper]** Przygotowanie środowiska do prezentacji dema.
        

---

### 6. Kwestia Dockera (Czy jest sens?)

**Tak, jest absolutnie sens.**

Pytanie nie brzmi "czy", tylko "jak". Przy takim stosie technologicznym (React + Python/API + Baza Danych) Docker jest kluczowy.

**Dlaczego jest sens:**

1. **Zarządzanie Usługami:** Masz co najmniej 3 oddzielne usługi (API, Baza, Frontend). `Docker Compose` pozwoli Kacprowi uruchomić _cały system_ jedną komendą (`docker-compose up`).
    
2. **Uniknięcie "U mnie działa":** Martyna nie musi instalować Pythona i FastAPI, a Kacper i Gaxbacbi nie muszą instalować Node.js i Reacta. Każdy pracuje w swoim kontenerze.
    
3. **Spójność Środowiska:** Wszyscy (i docelowo serwer demo) będą używać tej samej wersji Pythona, PostgreSQL i Node.js, co eliminuje błędy związane z różnicami w systemach operacyjnych.
    
4. **Łatwe Wdrożenie:** Przygotowanie dema będzie polegało na skopiowaniu plików i uruchomieniu `docker-compose up` na docelowej maszynie.
    

**Rola dla Kacpra (Team Lead):** Jako Team Lead, Kacper powinien wziąć na siebie przygotowanie plików `Dockerfile` dla API, `Dockerfile` dla Reacta (nawet jeśli to tylko serwer deweloperski) oraz pliku `docker-compose.yml`, który połączy to wszystko z bazą danych PostgreSQL.