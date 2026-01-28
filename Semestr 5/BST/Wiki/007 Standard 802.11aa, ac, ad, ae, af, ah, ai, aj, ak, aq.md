# Standard 802.11aa

# Robust streaming of Audio Video Transport Streams
## Rozszerzona Priorytetyzacja (Intra-Access Category Prioritization)

- lepszej jakości audio i video, czyli zmapowanie 802.1D priorytetów oraz 802.11e 
- zwiększa liczbę kolejek priorytetów z 4 do 6 
- Kategorie głos i Video zostały podzielone na strumienie  "podstawowe" i "alternatywne"
- Rozszerza EDCA
## GCR - Groupcast with Retries

1. Rozwiązuje problem przesyłania wideo do wielu użytkowników jednocześnie
2. Proponuje nowy mechanizm poza broadcast i direct multicast
3. Nazwa tego mechanizmu to właśnie GCR co powoduje że transmisja grupowa jest bardziej stabilna

## SCS - Stream Classification Service

1. Umożliwia bardziej elastyczne zarządzanie jakością usługi w sieci niż standardowe metody
2. Główne Zadania to:
	1.  Inteligentne odrzucanie - wykorzystuje bit DEI (Drop Eligibility Indicator), pozwala oznaczyć ramki jako mniej ważne, w przypadku zatłoczenia AP odrzuci te pakiety jako pierwsze
	2. Elastyczne Kolejkowanie - Zamiast polegać na sztywnych priorytetach, SCS pozwala na dowolne mapowanie strumienic (id po SCSID) do kolejek podstawowych lub alternatywnych

## OBSS - Overlapping Basic Service Set

- Rozwiązuje problem gdy kilka sieci działa na tym samym kanale w bliskim sąsiedztwie
- Standardowy mechanizm dostępu do kanału może zawodzić, gdy twoja sieć znajduje się fizycznie miedzy dwoma innymi sieciami, które się nie słyszą nawzajem

1. Wprowadzono mechanizm współpracy między AP:
	1. Raportowanie (QLoad) - punkty dostępowe wymieniają się informacjami o obciążeniu sieci i poziomie zakłóceń poprzez Beacon albo na żądanie
	2. Inteligentne sterowanie - na podstawie tych raportów AP mogą zmienić kanał na mniej obciążony lub dostosować harmonogram transmisji

# Standard 802.11ac

- Very High Throughput VHT
- The maximum available configuration: AP with 8 antennas and 4 stations with 2 antennas,
160 MHz channel width, 256-QAM modulation, 5/6 coding rate – each station can obtain
1,73 Gbps
## Statystyki

- Przepustowość do 6.93 Gbit/s
- Kanały transmisji są bardzo szerokie 80 MHz oraz 160 MHz opcjonalne
- Zwiększa ilośc strumieni przestrzennych do 8x8 
- Zwiększa modulacje do 256-QAM
	- w komercyjnych urządzeniach w paśmie 2.4GHz
- Wsparcie dla MU-MIMO
	- Możliwość równoległej transmisji od AP do 4 stacji downlink
	- Dedykowane do urządzeń mobilnych 
- 5GHz pasmo
- Zmiana RIFS (Reduced Inter-Frame Spacing) okresu czasowego z [[005 Standard 802.11j, k , n| 802.11n]] bardziej wydajną funkcją agregacji ramek  (1048575 octets (the maximum size of A-MPDU in IEEE 802.11n is only 65535 octets))
- Kompatybilność wsteczna z 802.11a oraz 802,11n

# Standard 802.11ad

- odpowiednik 802.11ac z ulepszeniem o 60 GHz pasma częstotliwości
- Very High Throughput 60  GHz
- Europa 57 - 66 GHz, USA i Kanada 57,05 - 64 GHz

1. Ogromna wydajność do 6.76 Gbit/s przy użyciu OFDM
2. Bardzo krótki zasięg fale tej częstotliwości są silnie tłumione przez ściany i inne efektywny zasięg to 10 m
3. Typy transmisji:
	1. Single Carrier - bardziej energooszczędny prędkość 4.62 Gbit/s (385 Mbps (π/2-BPSK modulation) up to 4,62 Gbit/s (π/2-16-QAM modulation))
	2. OFDM - najwyższa wydajność dla dużych transferów 64-QAM 
	3. Speed spectrum - najwolniejszy tryb sterujący 27.5 Mbit/s, π/2-DBPSK modulation
4. 2,5 Gbit/s (π/2-QPSK) dla oszczędzania energii

# Standard 802.11ae 

- Celem jest priorytetyzacja ramek zarządzania, aby nie zginęły wśród zwykłych danych

1. Problemem w starszych sieciach było to że ramki te były wysyłane w klasie Best Effort
2. Wtedy duże obciążenie równa się opóźnienie albo utrata
3. Definiuje też protokół sygnalizacyjny do wymiany polityk QoS między urządzeniami
## Mechanizm QMF 

- Pozwala na przypisanie ramkom zarządzającym odpowiednią kategorie usługi
- Dzięki czemu większość dostaje najwyższy priorytet Alternative Voice

# Standard 802.11af

- Zakres częstotliwości VHF i UHF (od 54 MHz do 790MHz)
- użycie technologii radia kognitywnego oraz użycie pomiarów aby odkryć dostępna pasma częstotliwości
- Jest możliwa dzięki temu standardowi realizacja operacji WLAN na paśmie zarezerwowanym dla Telewizji
- Warstwa fizyczna opiera się na 802.11ac
- Szerokość kanału od 6 do 8 MHz ( w zależności od kraju)
- MIMO z 4 strumieniami przestrzennymi z użyciem STBC kodów lub MU-MIMO
- Maksymalna dostępna przepustowość to 26.7 Mbit/s dla 6 i 7 MHz i 35.6 Mbit/s dla 8 MHz
	- 4 streams and 4 bonded channels, the maximum possible throughput is 426,7 Mbps for 6 and 7 MHz channels and 568,9 Mbps for 8 MHz channel
- Użycie GPS do zlokalizowania stacji bazowej jest wymagane
- USA pozwala na maksymalna moc transmisji równą 100 mW dla 6MHz lub 40 mW jeśli wykryje transmisje na sąsiednim kanale 

# Standard 802.11ah

- Zaprojektowany do komunikacji M2M (Machine to machine)
- Działa w paśmie poniżej 1 GHz 

## Cechy 

- Niskie zużycie energii zasięg - idealny dla czujników bateryjnych bo niska częstotliwość oraz dobre mechanizmy oszczędzania energii
- Skalowalność - jeden AP może obsługiwać tysiące stacji końcowych jednocześnie 
- Aby uniknąć kolizji przy tak dużej liczbie urządzeń wprowadzono podział na sektory w BSS
- Warstwa fizyczna bazuje na 802.11a/g
- Dostępnych jest 26 kanałów z których każdy daje przepustowość na poziomie 100 Kbit/s
- Stacje przekaźnikowe - możliwe użycie stacji przekaźnikowych do maksymalnie dwóch hopów
- Dwukierunkowe TXOP - w trakcie jednego okresu czasowego można nadawac w dóch kierunkach down i up

# Standard 802.11ai

- Wprowadzono procedure FILS (Fast Initial Link Setup) dla zabezpieczenia połączeń miedzy AP i stacja w bardzo krótkim oknie czasowym (>100 ms)
- Duża liczba stacji mobilnych użytkowników stale dołącza i opuszcza powierzchnie istniejącego ESS
- Otrzymanie adresu IP i natychmiastowy start wymiany ruchu z użyciem AP 
- Zmniejszenie ilości widomości potrzebnych do bezpiecznego połączenia z 27 do 4
- Czas procedury handover został zredukowany z 10 sekund do 0.5 sekundy
- Poprawa procedury handover kiedy zmieniamy AP z innym SSID
- Zmniejszenie ilości ramek zarządzania potrzebnych do asocjacji
- Wprowadzono usprawnienia w warstwie MAC redukujące liczbę ramek Probe Responses i optymalizujące skanowanie pasma zwiększa to przepustowość sieci o 20 - 50 procent

# Standard 802.11 aj

- adaptacja 802.11ad dla użycia w Chinach w CMMW ( Chinese Mili-Meter Wave) paśmie
- Modyfikacja warstwy Fizycznej i MAC aby pracować na 45 GHZ

# Standard 802.11 ak

- Integracja stacji z 802.11 do standardu 802.3 czyli Ethernet i usprawnienie funkcji mostkowania
- Precyzuje procedury pozwalające na tworzenie tranzytowych połączeń wewnętrznych w oparciu o standard 802.1Q kluczowe dla sieci przemysłowych 
# Standard 802.11 aq

- umożliwia wykrywanie usług przed nawiązaniem połączenia Pre-Association Discovery 
- Można pobrać listę dostępnych usług przed połączeniem z AP
