# Standard 802.11 p
- Sieci dla środowiska samochodowego zapewnia komunikacje pomiędzy urządzeniami poruszającymi się z prędkością 200 km/h
- Zawane też **WAVE**

# Statystyki 

- Zakres częstotliwości 5.855 - 5.905 GHz Europa oraz 5.85-5.925 GHz Stany
- Warstw fizyczna zabrana z 802.11 a 
- W dodatku do standardowego 20 MHz operuje również w 10 MHz 
- Dla komunikacji dalekich zasięgów maksymalna moc wyjściowa moze być zwiększona do 760 mW
- Przez to że czas połączenia jest krótki urządzenia tylko asocjują się z siecią nie uwierzytelniają
- Specjalny BSSID ukryty w DATA ramce a dokładniej w nagłówku 
- Ulepszony timing synchronization function aby wspierać globalny timing synchronization oparty o zewnętrzne źródła jak GPS
- Random MAC address
- MAC jest oparty o EDCA funkcje
# Standard 802.11 r 

- Fast Roaming
- Zmniejszenie czasu przełączania pomiędzy komórkami WLAN 
- Zapewniając poprawny QoS i bezpieczeństwo
## Cel

- VOIP 
- Zadaniem 802.11r jest skrócenie czasu przerwy w połączeniu do 50 ms 
- Kluczowe dla aplikacji czasu rzeczywistego takich jak rozmowy głosowe 
## Metoda 

- W standardowym roamingu szczególnie w przypadku Enetrprais stacje przy każdej zmianie AP musi łączyć się z serwerem RADIUS  co trwa długo 
- 802.11r pozwala na wygenereowanie kluczy kryptograficznych z wyprzedzeniem lub w sposób skrócony 
1. Over-the-Air
	- Stacja komunikuje się bezpośrednio z nowym AP, zanim jeszcze rozłączy się ze starym
	- Z użyciem FT-Authentication i FT-(Re)Association ramek i generuje klucz 
2. Over-the-DS
	- stacja komunikuje się z nowym AP za pośrednictwem starego AP przez siec kablową przydatne gdy sygnał jest słaby 
	- Te same ramki

# Standard 802.11 s

- Sieci Mesh/Kratowe 

## Budowa

1. Portal Mesh 
	- pracuje jako brama/most do zewnętrznych sieci

2. Mesh STA
	- zakłada połączenie peer z Mesh Portalem są soąsiadami
	- pełny uczestnik w WLAN Mesh services
3. Mesh AP 
	- Funkcjonalność MP, skolokowane z AP który zapewnie BSS servies
4. STA
	- Poza siecią Mesh 
	- Połączone z Mesh AP
## HWMP - Hybrid Wireless Mesh Protocol

- łączy dwa podejścia do wyznaczania tras 
- stosowany w sieciach Mesh
1. Reaktywne (On-demand)
	- używa intra-mesh routing dla optymalizacji
	- szuka ścieżki dopiero jak chce wysłać dane do innej stacji wewnątrz sieci
	- kiedy nie ma root portal albo nawet kiedy jest to może dać lepszą ścieżkę
	- oferuje świetną elastyczność w zmieniającym się środowisku
2. Proaktywne (Tree-based)
	- Kiedy root portal jest obecny tworzymy drzewo routingu vektorów dystansu 
	- Każdy węzeł zawsze zna drogę do wyjścia z sieci co eliminuje konieczność ciągłego wyszukiwania w trasy
	- Jest bardzo wydajne w przypadku stałego deploymentu sieci kratowej
## Inne

- Tryb adresacji opiera się na 6 polach w nagłówku MAC
- Nowy protokół dostępu zwany MCCA - Mesh Controlled Channel Access
	- integruje elementy wprowadzone w EDCA i HCCA
	- pozwala węzłom na rezerwację czasu transmisji, aby uniknąć kolizji wewnątrz sieci mesh
	- bardziej przewidywalne isochroniczne dostarczanie usług szczególnie w przypadku dużych ramek
- Procedura rozwiązująca problem bezpieczeństwa kiedy asocjujemy nową stacje do sieci mesh - AMPE (Authenticated Mesh Peering Exchange)


# Standard 802.11u

- umożliwia współprace z sieciami zewnętrznymi przede wszystkim komórkowymi 
1. Zrzucanie automatyczne ruchu danych z przeciążonej sieci komórkowej do Wi-Fi
2. Pozwala na integracje z systemami autoryzacji sieci komórkowych
3. Punkt dostępowy potrafi wysłać w jednej ramce rozgłoszeniowej lite dostępnych operatorów 
4. Wsparcie dla połączeń alarmowych

# Standard 802.11v

- Pozwala infrastrukturze sieciowej na konfigurowanie parametrów stacji 
1. Umożliwia wymianę informacji o topologii sieci, obciążeniu kanału i poziomie zakłóceń 
2. Wprowadza mechanizm oszczędzania energii
3. Optymalizuje ruch multicastowy

# Standard 802.11w 

- Celuje w uwierzytelnianie i szyfrowanie ramek zarządzania

1. Wprowadza definicje mechanizmów które zapewniają integralność danych, autentyczność pochodzenia danych, ochronę przed replay atakami i innymi np. rozłączaniem stacji z AP

# Standard 802.11y

- Zaprojektowany na rynek amerykański 

## Cechy

- Pasmo 3.6-3.7 GHz
- Pozwala na nadawanie z mocą do 20W
- Wprowadza mechanizm DSE - Dependent Station Enablement 
	- Stacje nie potrzebują licencji ale 
	- Są zależne nie mogą nadawać bez sygnału z stacji bazowej licencjonowanej
- Z powodu współdzielenia pasma z innymi wprowadzono mechanizm Contention Based Protocol - wymusza on na urządzeniach sprawdzanie dostępności kanału przed nadawaniem
- ECSA - ulepszony mechanizm informowania klientów przez AP o planowanej zmianie kanału lub jego szerokości co pozwala na płynne uciekanie przed zakłóceniami

# Standard 802.11z

- TDLS - Tunneled Direct Link Setup 
1. Definiuje mechanizm który pozwala 802.11 utworzyć bezpośrednie połączenie pomiędzy urządzeniami klienckimi pozostając zasocjowane z AP
2. Umożliwia dwóm urządzeniom podłączonym do tego samego AP (np. laptopowi i drukarce lub telewizorowi) zestawienie **bezpośredniego tunelu** radiowego między sobą.
3. Bez interwencji AP zestawiamy połączenie
4. Są chronione przez najwyższe możliwe standardy dostępne na urządzeniach klienckich
5. Definiuje ulepszony mechanizm oszczędzania energii