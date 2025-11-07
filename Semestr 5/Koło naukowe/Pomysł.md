**Temat: Pomysł na architekturę lokalizatora (Hybryda UWB + BLE)**

 Główny problem, jaki rozwiązujemy, to pogodzenie dwóch sprzecznych wymagań: **dokładności centymetrowej** i **bardzo długiej żywotności baterii** taga (naszej "upośledzonej pasywności").

Jak wiemy, samo UWB da nam precyzję, ale zajedzie baterię. Samo BLE (RSSI) da nam baterię, ale nie da precyzji.

Proponuję **architekturę hybrydową (UWB + BLE)**, która bierze najlepsze z obu tych światów.

## Jak to ma działać?

Koncepcja opiera się na dwóch trybach pracy taga:

### 1. Stan Głebokiego Uśpienia (99.9% czasu)

- Główny moduł UWB taga jest **całkowicie wyłączony** (zero poboru mocy).
    
- Aktywny jest **tylko moduł BLE** w trybie ultra-low-power.
    
- W tym stanie tag jedynie nasłuchuje na specjalny sygnał "pobudki" (wake-up call).
    
- **Efekt:** Zużycie energii jest minimalne, bateria może trzymać miesiącami/latami.
    

### 2. Stan Aktywnej Lokalizacji (Tylko na żądanie)

To dzieje się tylko wtedy, gdy użytkownik chce znaleźć taga:

1. **Start:** Użytkownik odpala naszą apkę na telefonie.
    
2. **Pobudka:** Apka wysyła przez BLE sygnał "pobudki" do konkretnego taga.
    
3. **Aktywacja UWB:** Tag, po odebraniu komendy BLE, **natychmiast wybudza swój moduł UWB**.
    
4. **Pomiar:** Przez krótki, zdefiniowany czas (np. 15-30 sekund) tag zaczyna aktywną komunikację (ping-pong / ToF) z kotwicami UWB w zasięgu.
    
5. **Obliczenia:** Kotwice zbierają pomiary, system liczy pozycję  i wysyła wynik do aplikacji użytkownika.
    
6. **Powrót do Uśpienia:** Po zakończeniu sesji (lub zerwaniu połączenia z apk), tag **automatycznie wraca do stanu głębokiego uśpienia** (pkt 1), aby oszczędzać energię.
    

---

## Kluczowe Korzyści

- **Precyzja:** Osiągamy cel centymetrowej dokładności, bo w momencie pomiaru używamy pełnej mocy UWB.
    
- **Żywotność Baterii:** Osiągamy cel "upośledzonej pasywności", bo tag zużywa znaczącą energię tylko przez te kilka-kilkanaście sekund, gdy jest aktywnie szukany.
    
- **Wykonalność:** Wygląda to na w pełni realizowalne przy użyciu gotowych komponentów (np. moduły ESP32 zintegrowane z UWB i BLE).
    
