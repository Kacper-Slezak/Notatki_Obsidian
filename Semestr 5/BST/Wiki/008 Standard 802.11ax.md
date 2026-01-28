- wifi 6, High Efficiency
- Dodano pasmo kanały w zakresie 5935 - 7125 zostały dodane 
	- Powiadomienia o operacjach 6 GHz za pomocą beacon w 5GHz
	- Limity 20 MHz kanałów aby redukować czas skanowania
- Modulacja 1024-QAM

## OFDMA - orthogonal frequency division multiple access

1. Pozwala na multipleksacje wielu użytkowników w domenie częstotliwościowo czasowej
2. Kanał radiowy dzielony jest na mniejsze pod kanały - Resource Unit
3. Zmniejsza to opóźnienie i zwiększa wydajność
4. Wsparcia dla uplinku oraz Downlinku 
5. Dla Uplinku wysyłany jest Trigger Frame który synchronizuje urządzenia i przydziela im RU
### OFDM
1. Czas trwania symbolu wydłużony do 12.8 us - odporność na opóźnienia i odbicia sygnału
2. Gęściej upakowane podnośne w kanałach 20 MHz z 64 dodo 256 (256 punktowa transformata FFT) - odstęp między podnośnymi jest 4 razy mniejszy
3. Z powodu dłuższego symbolu narzut czasowy na przerwę ochronną jest stosunkowo mniejszy co poprawia ogólną wydajność o 15 procent w dziedzinie czasu 
4. Podnośne na krawędziach widma co daje 5 procent zysku

## Spatial Reuse

- Mechanizm redukuje problem wyeksponowanego węzła i pozwala na agresywniejsze wykorzystanie pasma w miejscach jak stadiony czy bloki mieszkalne

#### Wydzielamy dwie główne techniki

1. OBSS-PD (Packet Detection) - stacja po wykryciu nośnej dynamicznie steruje mocą steruje się progiem detekcji po którym powinniśmy nie nadawać oraz steruje się mocą aby nie zakłócać sąsiadów nadających
2. SRP (Spatial Reuse Parameter) - nie dostosowujemy tu progu czułości dynamicznie ale działamy na predefiniowanych parametrach, AP wysyła parametry w Trigger ramce, jei stacja spełni warunki parametrów może nadawać na tle innej stacji\

## BSS Coloring

- pozwala na dodatkowo ponowne użycie kanału za pomocą koloru 
- Bardziej technicznie to pozwala on na szybkie odróżnienie transmisji pochodzących z sieci własnej od transmisji z sieci sąsiednich 
##### Zasady działania 

1. Identyfikator (Kolor) - AP przydziela stacji unikalny identyfikator zwany kolorem od 1 do 63 i jest on dołączany do preambuły każdej ramki
2. Urządzenie które nasłuchuje sprawdza ten identyfikator 
	- Jeśli kolor jest zgodny ramka jest przetwarzana standardowo
	- Jeśli inny, to sygnalizujemy zakłócenie z innej sieci obcej i przy małej mocy sygnału możemy tą transmisje ignorować nadając równolegle

#### Dwa liczniki NAV

- W związku z mechanizmem tym wprowadzono dwa oddzielne wektory alokacji sieci 
- Dla własnej sieci i sieci sąsiednich
- Aby rozpocząć nadawanie oba liczniki muszą pokazywać że kanał jest dostępny
## Ulepszenie MU-MIMO 

- dodanie uplinku dla Multi user MIMO
- Trigger ramka inicjuje uplink 
- Odpowiadamy an to za pomocą ACK, BlockACK i Multi STA Block ACK
## Ramka PHY

- na początku legacy preambuła pola standardowe STF STF LTF LTF SIG
	-  STF: Short Training Field LTF: Long Training Field SIG: Signal Field
- L-preambuła nie ma wsparcia 
- dodatkowo SU-MIMO 
- TODO!!!!!  

## Mechanizm oszczędzania energii - TWT Target Wake Time

### Działanie

1. Planowanie wybudzeń, zamiast budzić albo losowo albo na każdy BEACON, to AP i Stacja ustalają harmonogram kiedy urządzenie się wybudzi, aby wysłać i odebrać dane
2. Dzięki temu mamy dłuższy sen 
3. Redukcja kolizji - zmniejsza się natłok w sieci i ryzyko kolizji w przypadku wielu urządzeń nadających po wybudzeniu 
