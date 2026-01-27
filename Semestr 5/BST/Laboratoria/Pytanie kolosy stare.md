Z których technik korzysta Bluetooth:
- GFSK
- frequency hopping 
- retransmijse utraconych danych
Do czego służy iperf:
- Do pomiaru przepustowości udp tcp 
Jaki algorytm jest używany do tworznie 64 bitowego:
- RC4
Które narzędzi bezpośrednio służy do łamania kluczy WEP:
- aircrack-ng
Do czego służy oprogramowanie aireplay-mg?
- fake authentication
- atak ARP replay
- deauthentication
Sieci ad-hoc pracuje jako ?
 - IBSS - independent basic service set 
 Czym jest PTK w WPA/WPA2
 - kluczem szyfrującym sesje użytkownia
 Dlaczego trzeba odczekać losowy backoff?
 - W celu zmniejszenia ilości kolizji
 - W celu zapewnienia w miare sprawiedliwego dostępu do kanału
 Podczas pomiaru przepustowość TCP może dać inne wyniki niż udp bo ?
 - Większa nadmiarowość protokołu
 - W przypadku błędów transmisji 
 - Z powodu mechanizmu kontroli przeciążeń w TCP
 Wskaż ataki typu DoS?
 - fake authentication 
 - deuthenticantin
 - beacon flooding
 Jaką role pełni 4-way-handshake w WPA/WPA2?
 - generowanie tymczsowych kluczy szyfrujących
 - uwierzytelnianie stacji
 - uwierzytlenianie AP
 Wskaż profile bluetooth?
 - DUN - dial-up profile
 - HSP - headset profile
 - FTP - file transfer profile
 - HID - human interface device 
 - SPP - serial port profile
 Dlaczego wydajność sieci jest niska podczas przeysłania krórtkich ramek ?
 - Z powodu narzutu 802.11
 - Większa ilość ACK
 - Częste odliczanie backoff
 Nagłówek mac stadardu 802.11 ma?
 - 4 pola adresowe każde po 6B
 - zawiera informacje czy ramka jest retransmitowana
 Interfejs WLAN w trybie monitor ?
- jest niezbędny do działania większości narzędzi pakietu aircrack-ng
- pozwala analizować wszystkie odebrane ramki 802.11
Jakim polem zaczyna się nagłówek MAC ramek danych w ramach standardu ?
- Frame control
Cechy wyróżniające sieć ad-hoc?
- Brak wykorzystania AP
Jakie parametry są wykorzystywane do utworzenia kluczy szyfrujących w WPA/WPA2
- PSK
- BSSID
- Anonce
- Snonce
- SSID
- Mac nadawcy i odbiorcy
Czym jest szczelina czasowa ?
- jest to najkrótsza jednostka czasu  odliczana podczas procedury backoff oraz użyta pryz liczeniu difs pisf
Czym jest GTK w WPA/WPA2
- kluczem szyfrującym transmisje multicast broadcast
Czym jest PSK w WPA/WPA2
- Hasłem dostępu do sieci 
Co zawiera tablica bridge ?
- przypisanie interfejsów do mostów
Jakimi parametrami mogą się różnić sieci rozgłaszane przez jeden interfejs fizyczny ?
- SSID
- Sposób uwierzytelniania
- czy sieć jest ukryta
Wszytskie serwery/protokóly AAA?
- RADIUS 
- TACACS+
- DIAMETER
Które parametry opisują mechanizm backoff ?
- CWMAX
- CWMIN
- SLOT time
Jak powinna zachować się stacja która odbierze CTS od innej stacji?
- wszytrzymać wszytskei transmisje na czas określony w CTS duration 
Sytuacje w których korzystne jest zmian CWmin CWmax?
- Gdy jest dużo urządzeń w sieci -> Zwiększyć 
- Mała liczba urządzeń w sieci -> Zmniejszyć 
Za pomocą iptables można ?
- ustawić firewall 
- konfigurować NAT
- konfigurować dostęp do sieci WAN dla wybranych klientów
Czym się rózni większa i mniejsza sieć w warunkach nasycenia przy standardowym CW ?
- Większa sieć ma więcej kolizji
- Większa sieć ma więcej retransmiji
Czym jest DIFS?
- Czasem który musi odczekać każda stacja od momentu zwolninia kanału aby móc nadawać
Do czego służy airmon-ng?
- uruchomienia trybu monitor interfejsu WLAN
Wskaż warstwy protokołu bluetooth?
- L2CAP
- Baseband
- LMP
Ile jest pól adresowych w nagłówku MAC jaki jest ich rozmiar i funkcja ?
- pola są 4 po 6B jest receiver transmiter sourve destination
Czym jest WPA -Eneterprise?
- sposobem uwierzytelniani sieci z wykorzystaniem serwera NAS 
Czym jest i czemu słuzy repeater w sieciach WLAN ?
- jest to urządzen warstwy pierwszej 
- powtarza odebrane ramki w celu zwiększenia zasięgu sieci WLAN
Za pomocą modułu TC można ?
- konfigurować ograniczenia przepustowości dla wybranych klientów
- ograniczyc przepustowość dla wybranej sieci wirtualnej WLAN
Wskaż z których rozwwiązań może korzystac standard 802.11ac?
- MIMO
- Agregacje pakietów
- OFDM
- kanał o szerokości 80 
- kanał o szerokości 40
Tryb transmisji kodowanie i modulacja to ?
- MCS - modulation and coding schema
Jakie ramki wymienia między sobą stacja i ap w procesie przyłącznai sie  do sieci 
- probe req
- probe respond
- auth 
- association req
- association respond
Wektor inicjalizacyjny ma długośc ?
- 3B
Ramki RTS/CTS ?
- wspierają działanie mechanizmy NAV
- zawierają FCS - frame check sequence 
- należą do grupy ramek kontrolnych 
Jaki profil standardu Bluetooth jest używany w celu do zapewniania komunikacji miedzy komputerem i klawiatura
- HID 
Metoda wstrzykiwania pakietów do AP w celu złamania wep
- wymaga przejścia w tryb pracy monitor
Algorytm WEP?
- umożliwia użycie kluczy użytkownika o stałe jdługości 40 i 104 bitów
- szyfruje tekst jawny z apomca XOR struienia klucza
Parametr RTS_threshold ?
- powoduje stosowanie rezerwacji  wstępnej kanału radiowego dla wszytskichramek większych niż wartość parametru
Uruchomienie maskarady IP/NAT na kliencie umożliwia?
- podmniane źódłowych lub docelowych adrsów IP, zwykle też numerów portówTCP/UDP pakietó które przepływają przez urządzenie
Narzędzie badanie wydajności sieci Iperf:
- pracuej w trybe serwer kilent
- pozwala na analize wydajności sieci TCP/UDP
- klient może zestawić kilka sieci połączeń
- pozwala na pomiar zarówno jittera jak i strat 
Oprogramowanie Kismet?
- pasywnie wykrywa sieci WLAN
- potrafi wykryć sieci z ukrytym SSID
- jest oparte na architekturze kilent serwer
- potrafi dekodować ramki WEP w czasie rzeczywistym - tylko odszyforwac jka sie mu poda kluz nie łamać
Wymień warstwy bluetooth:
- L2CAP
- RFCOMM
- HCI
- Baseband
Pole adresowe Source w nagłówkju ramki WLAN
- informuje o adresie nadawacy ramki
- ma zawsze 6B
- może zawierać BSSID
- może zostac podmieniony
- może zostać spreparowane 
Która odmiana protokołu zapewnia najwyższy poziom bezpieczeństwa ?
- EAP-TLS
Oprogramowanie cruch pozwala na ?
- utowrzeni dowolnego słownika z okereśłonego zestawu znaków 
EAP-MD% vs PEAP?
- PEAP nie jest podany na ataki MITM EAP-MD% jest podatny 
- W EAP hasło jest wysyłąne za pomocą funkcji skrótu a w peap za pommocą tuenlu 
Tryb adhoc ?
- pozwal rozgłaszac SSID sieci 
- nie wymga AP
- inaczej nazwany IBSS
- w standarcie ac moze rozgłaszac kanały 80 mhz

