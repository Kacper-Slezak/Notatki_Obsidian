# Standard 802.11 f

## IAPP

- Wprowadzony w celu współpracy punktów dostępowych różnych producentów w ESS
- Działa na warstwie aplikacji ponad IP
- wysyła dane z użyciem TCP/UDP
- Aby wysłać coś do innego AP musi znać jego IP, zna adress MAC (BSSID) innego AP i odpytuje serwer radius o jego IP
#### ADD
1. Stacja przemieszcza się z jednego AP do drugiego no to ta informacja musi dotrzeć do tego jednego z nich, aby zrobili deasocjacje
#### MOVE

#### Cache



# Standard 802.11g

### Statystyki

- Operuje na 2.4GHz
- 3 ortogonalne kanały jak w [[001 Standard 802.11b| 802.11b]]
- Jest kompatybilny wstecznie z [[001 Standard 802.11b| 802.11b]]
- Przepustowość 22 Mbit/s za pomocą PBCC
- Używa CCK 802.11b modulacji co daje 1-11 Mbit/s
- Używa OFDM 802.11a modulacji co daje 6-4 Mbit/s
- AP wspiera 802.11b oraz 802..1g
- 802.11g i 802.11a 
- zasięg na 54 Mbit/s to 40 m

### Tryby pracy 

- ERP-DSS zapewnia kompatybilność wsteczną z 802.11b
- ERP-OFDM - jest odpowiednikiem standardu 802.11a w 2.4GHz
- ERP-PBCC - jest opcjonalne i pozwala na transmisje z prędkością 22 i 33 Mbit/s
- DSS-OFDM - tryb hybrydowy, pozwala używać DSS dla transmisji premabuły/nagłówka i OFDM dla payload
### PBCC (Packet Binary Convolutional Code)

- używa CCK do transmisji nagłówka i preambuły oraz PBCC do payloadu
- Rozwiązanie zwane 802.11b+ i nie jest uwzględnione w 802.11 standardzie

#### Długa preambuła PPDU format - DSSS-OFDM 

- Preamabuła oraz Nagłówek jest wysyłany z użyciem DBPSK
- Payload jest wysyłany z użyciem OFDM

#### Krótka preambuła PPDU format - DSSS-OFDM

- Preambuła to jest DBPSK
- Nagłówek to jest DQPSK 
- Payload OFDM 

# Standard 802.11h - Spectrum Managed

 - Odnosi się on do wymagań europejskich regulatorów dla urządzeń w paśmie 5GHz
 - Głównym celem jest zapobieganie zakłóceniom w pracy radarów i satelitów, którzy są uprzywilejowani w tym paśmie 
# DCS - dynamic channel selection

- wymaga aby urządzenia monitorowały widmo przed i w trakcie nadawania 
- Jeśli zostanie wykryty sygnał radaru musi przerwać transmisję przenieść się na inny kanał 

# TPC - transmit power control

- Kontrola mocy transmisji na poziomie 1mW z tolerancja do 5 dB
- pozwala na dynamiczne zarządzanie mocą 

# Standard 802.11 i

- Standard wprowadza RSM - Robust Security Network
- Laboratorium WPA WPA2 EAP RADIUS TKIP CCMP WPS i inne to ejst cął ystandard 