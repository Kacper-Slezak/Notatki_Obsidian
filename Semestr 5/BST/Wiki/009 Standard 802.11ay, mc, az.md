# Standard 802.11ay 

- Kolejna generacja sieci 60 GHz
- Rozwinięcie standardu [[007 Standard 802.11aa, ac, ad, ae, af, ah, ai, aj, ak, aq|ad]] 

1. Standard celuje w przepustowość 20 Gbit/s a teoretyczny maks to 250 Gb/s 
2. Funkcja Channel Bonding i Agregacja = pozwala na łączenie i agregacje sąsiednich kanałów co zwiększa dostępne pasmo transmisji
3. Wsparcie dla MIMO wspiera SU-MIMO oraz MU-MIMO(downlink) do 8 strumieni przestrzennych
4. Multiplexing polaryzacyjny - używa polaryzacji anten do wysyłania niezależnych strumieni danych używając polaryzacji
#### Zastosowania:

- bezprzewodowe wideo 8k
- systemy AR/VR
- stacje dokujace
- połączenia między szafami serwerowymi

# Standard 802.11mc

- Standard skupiający się na lokalizowaniu urządzeń i mierzeniu odległości
- wprowadził mechanizm Fine Timing Measurements (FTM)
	- zamiast polegać na mało precyzyjnej sile sygnału FRM mierzy czas przeloty sygnału w obie strony RTT 
	- na podstawie czasu obliczana jest odległość z dokładnością co do metra

# Standard 802.11az

- Ulepszony 802.11mc 
- Wyższa dokładność:
	- dzięki MIMO oraz szerszym kanale oferuje lepszą precyzje nawet w warunkach bez bezpośredniej widoczności
- Oprócz czasu mierzy również kąt nadejścia i kąt odejścia sygnału i jego faze co pozwala na triangulację
- Bezpieczeństwo
	- Wprowadza mechanizmy chroniące przed fałszowaniem lokalizacji
	- poprzez zabezpieczenie sekwencji pomiarowych w warstwie fizycznej
- Pasywna lokalizacja - lokalizowanie wielu użytkowników jednocześnie bez generowania dodatkowego obciążenia sieci dla każdego z nich z osobna 

# Standard 802.11ba

- Wake-up Radio 
- Poprawia wydajność energetyczną i utrzymuje niskie opóźnienie 
## Mechanizm

- Urządzenie jest wyposażone w drugie dodatkowe radio jako odbiornik 
- Standardowe prądożerne radio zostaje stale wyłączone
- LP-WUR jest cały czas aktywny, ale zużywa śladowe ilości energii 
- LP-WUR wykorzystuje modulacje OOK (On-Off Keying) i wąskie pasmo < 5MHz

# Standard 802.11bb

- Light Communications - Light Fidelity Li-Fi technology 
- Zamiast sygnałów radiowych używa zmodulowanych fal światła do transmisji danych
- Modulowane jest intensywność aby kodować dane 
- Dwukierunkowa komunikacja
	- fale podczerwone dla uplink
	- widzialne lub podczerwone dla downlink
- Modulacja OOK - On-Off Keying - włącza i wyłącza źródło światła 
- Modulacja pozycji pulsu -= pozycja impulsu w czasie koduje dane 
- OFDM - dzieli sygnał na wiele podpasm 
- Zastosowania:
	- Przemysłowe bezprzewodowe aplikacje
	- Medyczne środowisko
	- Enterprise
	- Home 
	- Pojazd do Pojazdu komunikacja
	- Podwodna Komunikacja
- Dodatki
	- 380 nm do 5 000 nm pasmo
	- Minimum pojedynczego łacza przepustowość to 10 Mbit/s
- Warstwa MAC może płynnie przełączać się między łączem radiowym a świetlnym
	- 802.11a to bazowe dla PHY

# Standard 802.11bc

- Definiuje Enhanced Broadcast Services (eBCS)
1. Jest możliwy broadcast uplink i downlink
2. Zero Setup automatyczne przesyłanie danych do serwera przez dowolny AP bez konieczności skomplikowanej konfiguracji czy parowania

# Standard 802.11bd

- Ewolucja standardu 802.11[[006 Standard 802.11p,r,s,u,v,w,y,z | p]]
- Vehicle to Anything
- Działa głównie na 5.9 GHz i opcjonalnie 60 GHz
- Lepsze osiągi dzięki
	- OFDM ramką
	- Wyższym MCS 
	- LDPC kodowanie
	- Agregacja pakietów
- Większy zasięg 
- Wsparcie dla pozycjonowania
- Kompatybilność wsteczna


# Standard 802.11be

- Extremely High Throughput (EHT)

## Statystyki

- Operuje na paśmie 2.4GHz, 5GHz, oraz 6GHz
- Przepustowość - 46 Gbit/s
- Szerokość kanałów do 320 MHz
- Modulacja 4096-QAM ( zwiększa przepustowość o 20% względem 1024-QAM)
- MU-MIMO uplink i downlink
- Strumienie przestrzenne 16 
- Wsparcie dla komunikacji o niskim opóźnieniu
- SNR potrzebny do odebrania to około 40 dB  dzięki beamforming
- Ulepszony protokół adaptacji łącza i retransmisji HARQ

## OFDMA 

1. Wielokrotny RU (MRU) - W poprzednim standardzie Wi-Fi 6 stacja mogła otrzymać tylko jedną jednostkę zasobów RU, tutaj wprowadzono wiele jednostek do jednej stacji 
2. AP steruje transmisją w dół i w góre

### Dziurkowanie (Preamble puncturing) 

- Kluczowy dla szerokich kanałów
- jeśli fragment pasma jest zajęty przez zakłócenie AP mogą go wyciąć i transmitować przez inne części pasma
- kluczem jest to że te informacje są sygnalizowane w preambule fizycznej
- EHT preambułą zawiera bitmap dziurek
	- odbiorca wie przez które małe kanały 20 MHz jest transmitowana informacja 

#### Przebieg

- Wykrywamy nośną na każdym z 20 MHz pod kanałów
- Tworzymy bitmap 
- Transmitujemy preambule EHT z zakodowaną informacją o szerokości kanału, strumieniach przestrzennych oraz bitmap
- OFDM symbole są transmitowane
- Stacja dekoduje i nasłuchuje tylko na wybranych podpasmach
- Pierwszy kanał musi być wolny (Primary 20 MHz)

## Wsparcie dla 16 strumieni przestrzennych

- Naiwne pozyskanie CSI - tradycyjny explicit Feedback generuje zbyt duży narzut przy 16 strumieniach
- Tutaj szacuje się stan kanału na podstawie normalnych sygnałów odebranych od klienta jest to zjawisko wzajemności kanału
- Eliminuje to zbędny ruch 
- Lepsza kalibracja RF i bardziej dokładne EHT preambuły 

## HARQ - Hybrid Automatic Repeat Request 

- Zaawansowany mechanizm korekcji błędów 
- W tradycyjnym ARQ jeśli suma kontrolna się nie zgadza to do kosza 
- W HARQ zachowujemy uszkodzoną ramkę
- Gdy mamy retransmisje odbiornik łączy sygnał z pierwszej próby z nowym sygnałem
- HARQ daje zysk rzędu 4 - 6 dB w SNR

## Koordynacja wielu AP

- Architektura slave/master w AP
- AP przestają konkurować zaczynają współpracować 
- Wymieniają się informacjami o stanie kanału (CSI), buforach, harmonogramach
- Kilka typów
	1. Coordinated Beamforming (CBF) - nadają nie zależnie do swoich klientów ale koordynują kształt wiązki radiowej, AP steruje sygnałem aby celowo stworzyć dziurę w kierunku sąsiada
	2. Joint Transmission - wiele punktów dostępowych wspólnie nadaje ten sam strumień danych do jednej stacji działając trochę jak rozproszone MIMO
	3. Coordinated OFDMA - AP wygrywający dostęp do kanału może odstąpić nie wykorzystane podnośne RU sąsiedniemu AP

### Skoordynowane ponowne użycie przestrzenne 

 - Decyzja o nadawaniu polegała na mocy sygnału OBSS_PD / Color BSS - jeśli zakłócenie było słabe urządzenie nadawało 
 - Punkty dostępowe wspólnie planują transmisje 

# Standard 802.11bf

- WLAN sensing 
- urządzenia wi-fi potrafią wykryć obecność i ruch obiektów lub ludzi w otoczeniu na podstawie analizy zmian w sygnale radiowym bez konieczności noszenia przez nich jakichkolwiek urządzeń
- Zastosowanie:
	1. Detekcja bez kontaktowa 
	2. Smart Home - automatyka 
	3. Zdrowie - wykrywanie oddechu, tętna lub wykrywanie upadków
	4. Interfejsy - sterowane za pomocą gestów
- Pasmo od 1 GHz do 7.125 GHz oraz pasmo milimetrowe poniżej 45 GHz 

# Standard 802.11bf

- Losowy i zmieniający się adres MAC (RCM)
- Cel to kompromis między prywatnością użytkownika oraz poprawnym identyfikowaniem
- Losowy adres MAC powoduje problemy z zarządzaniem oraz dostępem do usług 

# Standard 802.11bi

- Ulepszona prywatność danych
- Ograniczenie możliwości śledzenia użytkownika i urządzeń
- Bada nowe mechanizmy które zapobiegają identyfikacji urządzeń przez analizę pól w warstwach PHY i MAC 
- Ukrywanie identyfikatorów za pomocą technik kryptograficznych 

# Standard 802.11bn

- WiFi 8 
- Ultra High Reliability 
## Założenia

- Distributed MLO - klient może utrzymywać kilka połączeń jednocześnie z wieloma fizycznie oddzielonymi punktami dostępowymi
- Zwiększenie przepustowości o 25%
- Redukcja opóźnień 
- Redukcja utraty pakietów
- Koordynacja między wieloma AP
- Priorytet dla niskich opóźnień
- SCA - Secondary Channel Access - rozwinięcie dziurkowania preamble puncturing 