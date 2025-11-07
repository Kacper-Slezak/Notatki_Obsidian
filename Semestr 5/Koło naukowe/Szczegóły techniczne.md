

**Temat: Propozycja architektury technicznej (Hybryda UWB/BLE) - Szczegóły implementacyjne**

W nawiązaniu do przedstawionej koncepcji systemu (hybryda UWB na żądanie + BLE wake-up), poniżej zaprezentowano proponowany stos technologiczny oraz szczegóły implementacyjne do dalszej analizy.

## Proponowany Stos Technologiczny

### 1. Tag (Urządzenie mobilne)

- **MCU + BLE: Platforma ESP32 (np. C3, S3)**
    
    - **Uzasadnienie:** Platforma oferuje zaawansowane, energooszczędne tryby głębokiego uśpienia (deep-sleep), zintegrowany moduł BLE do nasłuchu sygnału "wake-up call" oraz wystarczającą wydajność obliczeniową do obsługi modułu UWB. Atutami są również rozbudowany ekosystem i korzystny stosunek ceny do możliwości.
        
- **Moduł UWB: Qorvo DWM3000 (lub kompatybilny)**
    
    - **Uzasadnienie:** Jest to sprawdzony chipset zgodny z IEEE 802.15.4z, przeznaczony do pomiarów TWR (Two-Way Ranging). Kluczowym wymaganiem implementacyjnym jest zapewnienie możliwości całkowitego odcięcia zasilania od tego modułu przez MCU (np. za pomocą tranzystora MOSFET lub dedykowanego pinu EN), aby osiągnąć zerowy pobór prądu w stanie uśpienia.
        

### 2. Kotwica (Infrastruktura)

- **MCU + Łączność: Platforma ESP32 (z Wi-Fi lub Ethernet)**
    
    - **Uzasadnienie:** Wymagana jest stała, niezawodna komunikacja z systemem backend (przez Wi-Fi lub Ethernet/PoE). ESP32 zapewnia wymaganą elastyczność oraz wydajność do obsługi komunikacji UWB i agregacji danych.
        
- **Moduł UWB: Qorvo DWM3000**
    
    - **Uzasadnienie:** Zastosowanie tego samego modułu co w tagu zapewni pełną kompatybilność i symetrię pomiarów.
        
- **Kluczowy aspekt: Synchronizacja**
    
    - Precyzyjna synchronizacja czasu między kotwicami jest niezbędna w przypadku wyboru metody TDoA (Time Difference of Arrival).
        
    - W przypadku metody TWR (Two-Way Ranging), synchronizacja nie jest krytyczna dla samego pomiaru odległości. Proponuje się rozpoczęcie implementacji od TWR, co znacząco upraszcza architekturę systemu, kosztem dłuższego czasu aktywnej komunikacji taga.
        

## Architektura Przepływu Danych

### Stan 1: Deep-Sleep (Tryb nasłuchu BLE)

1. **Tag:** Główny MCU (ESP32) przechodzi w tryb `deep-sleep`.
    
2. Moduł UWB (DWM3000) jest **całkowicie odcięty od zasilania** (VCC = 0V).
    
3. Aktywny pozostaje jedynie koprocesor ULP (Ultra-Low-Power) w ESP32 lub sam rdzeń BLE, nasłuchujący na specyficzny pakiet BLE (np. dedykowany pakiet broadcastowy).
    
4. **Docelowy pobór prądu:** Rząd pojedynczych mikroamperów ($\mu A$).
    

### Stan 2: Aktywacja i Pomiar (Tryb "UWB on-demand")

1. **Inicjacja (Frontend -> Backend):** Użytkownik w aplikacji mobilnej wysyła żądanie lokalizacji taga (np. przez HTTP/MQTT) do serwera.
    
2. **Rozgłoszenie "Wake-Up" (Backend -> Kotwice -> BLE):**
    
    - Serwer identyfikuje kotwice w prawdopodobnym zasięgu taga (lub wysyła żądanie do wszystkich).
        
    - Wyznaczone kotwice (poprzez swoje moduły BLE) rozpoczynają emisję specjalnego pakietu "Wake-Up" zawierającego unikalny identyfikator taga do wybudzenia.
        
3. **Pobudka Taga (BLE -> MCU):**
    
    - Moduł BLE taga wykrywa adresowany do siebie pakiet "Wake-Up".
        
    - Generowane jest przerwanie (interrupt), które wybudza główny rdzeń ESP32 ze stanu `deep-sleep`.
        
4. **Aktywacja UWB (MCU -> UWB):**
    
    - ESP32 podaje zasilanie na moduł DWM3000 i inicjalizuje go (konfiguracja SPI, kalibracja). Czas startu modułu jest tu krytycznym parametrem.
        
5. **Ranging (UWB <-> UWB):**
    
    - Tag rozpoczyna sekwencję pomiarową TWR (np. SS-TWR lub DS-TWR) z kotwicami w zasięgu.
        
    - _(Alternatywa TDoA: Tag emitowałby jedynie sygnały "blink", co wymagałoby zaimplementowanej synchronizacji kotwic)._
        
6. **Agregacja (Kotwice -> Backend):**
    
    - Każda kotwica, po uzyskaniu pomiaru TWR, wysyła zmierzony dystans do serwera (np. przez MQTT).
        
    - _Przykład komunikatu:_ `{"anchor_id": "A1", "tag_id": "T123", "distance_cm": 1245}`
        
7. **Obliczenia (Backend):**
    
    - Serwer zbiera pomiary dystansu (wymagane min. 3-4 kotwice do lokalizacji 2D/3D).
        
    - Uruchamiany jest algorytm multilateracji (np. metoda najmniejszych kwadratów) w celu obliczenia pozycji ($x, y, z$) taga.
        
8. **Prezentacja (Backend -> Frontend):** Obliczona pozycja jest wysyłana do aplikacji użytkownika.
    
9. **Powrót do Uśpienia (Tag):**
    
    - Po wykonaniu zdefiniowanej liczby pomiarów (lub po upłynięciu ustalonego czasu sesji, np. 15 sekund), MCU taga automatycznie odcina zasilanie od modułu UWB i powraca do stanu `deep-sleep`, oczekując na kolejny sygnał "Wake-Up".
        

---

## Kluczowe Wyzwania Techniczne do Dyskusji

1. **Optymalizacja mechanizmu "Wake-Up":** Należy zdefiniować źródło sygnału "wake-up" (kotwice vs. telefon użytkownika) oraz zoptymalizować jego latencję. Wykorzystanie kotwic do emisji sygnału wydaje się rozwiązaniem bardziej stabilnym i niezależnym od urządzenia końcowego użytkownika.
    
2. **Zarządzanie sesją UWB:** Konieczne jest precyzyjne zdefiniowanie warunków zakończenia aktywnej sesji pomiarowej taga (stały czas, liczba pomiarów, zerwanie połączenia z aplikacją) w celu maksymalizacji oszczędności energii.