
## Skrypt Prezentacji: Projekt Hybrydowego Lokalizatora UWB + BLE

Dzień dobry. Chciałbym przedstawić Państwu koncepcję projektu, nad którym pracujemy – systemu lokalizacji wewnątrz pomieszczeń, który rozwiązuje jeden, fundamentalny problem, czyli "Zgubiłem, ale wiem, że jest w domu".

### 1. Problem: Dwa sprzeczne cele

Każdy, kto myśli o lokalizatorze, staje przed wyborem: albo chce mieć **dokładność**, albo **długą żywotność baterii**. Te dwie rzeczy są niemal zawsze w konflikcie.

Początkowo myśleliśmy o wykorzystaniu siły sygnału, czyli RSSI, na przykład z Bluetoot/WiFi. To proste i tanie. Ale po głębszej analizie stało się jasne, że to ślepy zaułek. Dlaczego? Bo siła sygnału jest ekstremalnie zawodna. Ściana, mebel, a nawet przechodząca osoba potrafi całkowicie zaburzyć odczyt. Tą metodą uzyskamy dokładność rzędu kilku metrów, a naszym celem jest **dokładność centymetrowa**.

### 2. Rozwiązanie (Część 1): Wybór właściwej technologii

Aby osiągnąć centymetrową precyzję, musimy odejść od pomiaru _siły_ sygnału na rzecz pomiaru _czasu_ jego przelotu. Wiemy, z jaką prędkością porusza się fala radiowa; jeśli precyzyjnie zmierzymy czas, precyzyjnie obliczymy dystans.

Technologią stworzoną do tego celu jest **Ultra-Wideband (UWB)**. Używa ona ultraszerokiego pasma i bardzo krótkich impulsów, co daje jej dwie kluczowe zalety: po pierwsze, niesamowitą rozdzielczość czasową, a po drugie, gigantyczną odporność na odbicia od ścian.

### 3. Rozwiązanie (Część 2): Architektura hybrydowa

Mamy więc UWB, które daje nam precyzję. Ale jest nowy problem: UWB jest energochłonne. Gdyby nasz tag działał non-stop, bateria zniknęłaby w oczach.

I tu dochodzimy do sedna naszego projektu: **architektury hybrydowej**. Łączymy to, co najlepsze w UWB, z tym, co najlepsze w Bluetooth Low Energy.

Jak to działa w praktyce?

- **Przez 99,9% czasu** nasz tag jest w stanie głębokiego uśpienia. Moduł UWB jest **całkowicie odcięty od zasilania**. Działa tylko moduł BLE, który nasłuchuje, pobierając przy tym minimalną energię.
    
- **Dopiero gdy użytkownik** chce znaleźć tag i odpala aplikację w telefonie, dzieje się magia.
    
- System (przez kotwice lub telefon) wysyła przez BLE specjalny sygnał "Wake-Up Call" (pobudki).
    
- Tag odbiera ten sygnał, wybudza swój główny procesor, który **dopiero teraz podaje zasilanie na moduł UWB**.
    
- Przez następne 15-30 sekund tag aktywnie komunikuje się z kotwicami UWB w pomieszczeniu, mierząc dystans metodą Time-of-Flight.
    
- Kotwice przesyłają te pomiary do serwera, serwer oblicza pozycję (x, y) za pomocą multilateracji i wysyła ją do aplikacji.
    
- Po sesji, tag automatycznie wraca do stanu głębokiego uśpienia.
    

Dzięki temu mamy i precyzję UWB (bo używamy jej, gdy jest potrzebna), i żywotność baterii (bo przez resztę czasu tag śpi).

### 4. Czego potrzebujemy (Technologia i plan)

Mamy też jasno określony stos technologiczny, który pozwoli to zrealizować.

1. **Tagi i Kotwice (Sprzęt):** Nie wyważamy otwartych drzwi. Bazujemy na sprawdzonych komponentach. Jako "mózg" operacji wybraliśmy **ESP32** – jest tani, ma świetne zarządzanie energią (tryby deep-sleep) i wbudowane BLE. Do precyzyjnych pomiarów UWB dołączymy do niego moduł **Qorvo DWM3000** – to standard branżowy, zgodny z IEEE 802.15.4z.
    
2. **Oprogramowanie (Plan):** Projekt podzieliliśmy na cztery jasne fazy. Zaczniemy od prostej komunikacji i pomiaru odległości między dwoma urządzeniami. Następnie przejdziemy do systemu z trzema kotwicami i algorytmu multilateracji, aby obliczyć pozycję 2D. Na końcu stworzymy wizualizację tych danych w czasie rzeczywistym, np. w Pythonie.
    

Podsumowując, proponujemy architekturę hybrydową, która jest kompromisem idealnym. Wykorzystuje UWB tylko na żądanie, a przez resztę czasu oszczędza baterię dzięki BLE. Jest to nasz pomysł po odrobinie research'u, ale jesteśmy bardzo otwarci na wszystkie propozycje optymalizacji lub uwagi  i pytania 