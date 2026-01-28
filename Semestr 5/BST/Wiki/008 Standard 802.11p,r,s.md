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