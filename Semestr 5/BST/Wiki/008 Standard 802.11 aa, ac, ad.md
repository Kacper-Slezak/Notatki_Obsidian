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
- Zmiana RIFS (Reduced Inter-Frame Spacing) okresu czasowego z [[006 Standard 802.11j, k , n| 802.11n]] bardziej wydajną funkcją agregacji ramek  (1048575 octets (the maximum size of A-MPDU in IEEE 802.11n is only 65535 octets))
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

- Celem jest priorytetyzacja ramek zarządzania
- 