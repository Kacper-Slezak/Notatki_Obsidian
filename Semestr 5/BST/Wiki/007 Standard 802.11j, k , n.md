# Standard 802.11 j

- Zostało dopracowane dla regulacji w Japonii

## Specyfikacja

- Zakres częstotliwości to 4.9-5GHz
- Obsługa kanałów o szerokości 10MHz
- Redefinicja parametrów czasowych np. Slot Time
## Zastosowanie

- Dedykowane do HotSpotów 
- Oraz stacjonarnych łączy szerokopasmowych Fixed Wireless Access pod kontrolą japońskich operatorów
- Ma nie zakłócać innych systemów w tym paśmie

# Standard 802.11 k

- Koncentruje się na pomiarach zasobów radiowych

## Roaming - optymalizacja

- Normlanie Stacja łączyła się z AP o najsilniejszym sygnale co może prowadzić do przeciążeń jednego AP a inne nie wykorzystane
- 802.11k pozwala przekierować klienta do mniej obciążonego pomimo słabszego sygnału da on lepszą przepustowość
- Działa to na zasadzie raportów stacja przed zmianą AP pyta go o listę sąsiednich AP dzięki czemu klient wie dokładnie na jakim kanale pracują 

## Pomiary

- Standard definiuje ramki 
- Measurement Request i Measurement Raport
- Pozwala to na zbieranie szczegółowych statystyk jak: pomiar szumów, obciążenie kanału, retransmisje

### Inne

- najczęściej współpracuje z 802.11r oraz 802.11v - tworząc system płynnego roamingu


# Standard 802.11n 


- Very high data rates 
- Ulepszony w oparciu o MIMO
## Statystki

- Max przepustowość 300 (600) Mbit/s
- Typowa 74 Mbit/s
- Pracuje na częstotliwości 2.4 GHz oraz 5 GHz
- Zasięg wewnątrz 70 m na zewnątrz 250 m
- Technologia MIMO
- Kompatybilność wsteczna dla a/b/g
## Zmiany

- Oparty o 802.11g

1. Więcej podpasm:
	- 802.11g miał 48 OFDM 
	- 802.11n ma 52 OFDM co zwiększa z 54 do 58.5 Mbit/s
2. FEC - Forward Error Correction
	- System sterowania błędem dla transmisji danych
	- Transmitujacy dodaje nadmiarowe informacje do wiadomości
	- Na ich podstawie możemy jako odbierający 
	- Wykrywać oraz Poprawiać Błędy bez potrzeby pytania o dodatkowe dane'
	- Zakodowane zwykle za pomocą BCC - binary constitutional code lub LDPC - low density parity check codes 
	- W zależności od wartości pola LDPC wybieramy encoder
	- Wprowadzono sprawniejszy współczynnik kodowania korekcyjnego (FEC) 5/6 co zwiększa do 65 Mbit/s z 58.5
3. Guard Interval - przerwa ochronna między symbolami
	- w 802.11g wynosiła 800ns
	- w 802.11n ma opcje redukcji do 400 ns co daje wzrost z 65 Mbit/s do 72.2 Mbit/s
4. **MIMO** - Multiple Input multiple Output multipleksacja przestrzenna
	- dzięki zastosowaniu wielu anten 4 po stronie nadawczej i odbiorczej 
	- możemy odbierać i nadawać wiele strumieni jednocześnie 
	- przepustowość wzrasta liniowo z dodatkowymi antenami na obu końcach
	- Teoretycznie daje do 72.2 razy 4 w szczycie ale praktycznie jest to mniej
5. 40 MHz kanały
	- Wszystkie poprzednie wersje 802.11 miały szerokość kanału równą 20MHz
	- w opcjonalnym trybie można w 802.11n zastosować 40 MHz jest to kontrowersyjne i mało praktyczne 
	- pozwala to zwiększyć bazowe 52 do 108 dodając inne ulepszenia około 150 
	- Co razem z MIMO daje możliwe 600 Mbit/s do uzyskania

## Dodatkowo

1. Mniejszy narzut MAC 
	- w 802.11 a/g prędkość t o54 Mbit/s, ale wyższe warstwy to tylko 26 Mbit/s narzut MAC = 54%
	- w 802.11 n kiedy prędkość to 65 Mbit/s to wyższe warstwy to około 50 Mbit/s więc narzut MAC = 25%
	- Zostało to osiągnięte przez zmiane ramki oraz agregacje 
	- Ramki są większe bo wiele ramek Ethernet MSDU jest agregowane w jedną dużą ramkę
2. Szybsza odpowiedź MCS 
	- Wcześniejsze systemy zmieniały prędkość (Rate Adaptation) dopiero po wystąpieniu błędów transmisji. 802.11n wprowadziło mechanizm, w którym odbiornik aktywnie podpowiada nadajnikowi, jakiej prędkości użyć dla następnego pakietu (szacując jakość kanału).
3. LDPC - Low Density Parity Check 
4. Transmit Beamforming 
	- Punkt dostępowy wykorzystuje wiele anten aby sterować fazą i mocą sygnału  
	- Daje to możliwość względnego sterowania wiązką w kierunku klienta
5. STBC - Space time Block Coding
