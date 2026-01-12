
## Lab 04: DoS i Uwierzytelnianie

1. Jaki jest cel i działanie ataku _fake authentication_?.
    
2. Na czym polega atak _Beacon flooding_?.
    
3. Do czego używamy narzędzia MDK3 podczas laboratorium?.
    
4. Wyjaśnij pojęcie _Zulu_ i jaki atak wykorzystuje ramki RTS.
    
5. Czym jest CTS/RTS i jak można je wykorzystać do ataku?.
    
6. Na czym polega atak za pomocą manipulacji $CW_{min}$ i $CW_{max}$?.
    
7. Jaka jest różnica między _monitor mode_ a _managed mode_?.
    
8. Do czego służy _iperf_?.
    


---
Co to jest za atak fake authentication Czym jest zulu
Czym jest cts i jak można go użyć do ataku? Czym jest iperf
atak beacon flooding atak za pomocą Cwmin i Cwmax
Różnica między monitor mode a managed mode Do czego używamy w trakcie laboratorium mdk3
Wejściówka
● Grupa 1
○ Cel i działanie fake authentication - Jest to kolejny rodzaj ataku DoS
typowy dla sieci WiFi. Stacja atakująca uruchamia liczne procedury
kojarzenia sieci na docelowym AP, a w pamięci RAM AP tworzony jest rekord
fałszywej stacji dla każdej takiej próby. Może to zostać wykorzystane do
przeciążenia pamięci w celu obniżenia jakości lub wyłączenia działania
docelowego punktu dostępowego. Atak może być skuteczny pomimo
stosowania klucza sieciowego lub filtrowania adresów mac.
○ Do czego służy iperf - sprawdzanie wydajności sieci
● Grupa 2
○ Do czego jest MDK3 - wstrzykiwanie pakietów, beacon flooding
○ Do czego służy RTS i jaki atak wykorzystuje RTS - RTS to prośba o
wysłanie pakietu, wykorzystywany w ataku z fałszywymi ramkami RTS (zulu)
● Grupa 3
○ Atak Beacon flooding jest rodzajem ataku DoS dostępnym w sieciach
WLAN. Polega on po prostu na sfałszowaniu wielu fałszywych ramek beacon,
co dezorientuje użytkowników w obszarze ataku, dając im informację o
istnieniu fałszywych sieci WiFi.
○ Do czego służy Zulu - do ataku fałszywymi ramkami RTS