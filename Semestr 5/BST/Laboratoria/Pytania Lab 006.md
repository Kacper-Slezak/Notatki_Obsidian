## Lab 06: Mostkowanie (Bridge) i Routing

1. Co to jest _bridge_ i czym różni się od routingu?.
    
2. Wytłumacz pojęcie _bridge tables_.
    
3. Co to jest _iptables_, _prerouting_ i _postrouting_? Co one robią?.
    
4. Wyjaśnij pojęcie interfejsu wirtualnego.
    
5. Wyjaśnij pojęcie TC (Traffic Control).
    
6. Jakich protokołów warstwy aplikacji możemy użyć do połączenia się z DD-WRT?.
    



---
1 co to bridge I czym się różni od rutingu 2 iptables
wytłumacz bridge tables TC
Czym jest interface wirtualny Jakie protokołu warstwy aplikacji możey uzyc do połączenia się z ddwrt
Co to ddwrt Co to jest prerouting i postrouting i co robi

Wejściówka
● Grupa 1
○ PEAP
wymaga certyfikatu serwera, korzysta z tunelu TLS do uwierzytelnienia
klienta (w środku MSCHAPv2)
○ Architektura RADIUS
● Grupa 2
○ EAP-TLS
jak PEAP tylko wymaga jeszcze certyfikatu klienta, trudny w implementacji
ale bezpieczny
○ Do czego służy hostapd-wpe
allows us to create a virtual AP out of a wireless interface
● Grupa 3
○ MSCHAPv2
protokół Challenge-Handshake Authentication od Microsoftu; używany np. w
PEAP
○ Do czego służy authenticator i typy urządzeń, które mogą nim być
access point or switch that mediates the exchange of information between the
supplicant and the authentication server, and ultimately assigns or denies
access to the network for the supplicant on the basis of information received
from the server