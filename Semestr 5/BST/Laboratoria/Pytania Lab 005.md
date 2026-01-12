
## Lab 05: WPA/WPA2 i Handshake

1. Dlaczego WPA2 jest lepsze od WPA?.
    
2. Jak przechwycić _4-way handshake_?.
    
3. Co jest ustalane podczas handshake'u (GTK, PTK)?.
    
4. Jakie są funkcje _4-way handshake_? Narysuj wymianę pakietów.
    
5. Wyjaśnij skrót PMK i opisz do czego służy.
    
6. Wyjaśnij pojęcie GTK.
    
7. Jakie wady ma WPS z PINem?.
    
8. Ile jest możliwości na klucz WPS?.
    
9. Opisz WPS PBC (Push-Button-Connect).
    
10. Jak łamać hasła WPA/WPA2?.
    
11. Dlaczego nie należy używać popularnych SSID?.
    
12. Jak _tablice tęczowe_ przyspieszają łamanie i dlaczego są zależne od SSID?.
    
13. Czym jest _Pyrit_?.
    


---
Grupa 1: Rozwinięcie skrótu PMK i do czego służy Jak przechwycić 4-way **handshake**
Grupa 9:45: 1. Rozwin WPS i ile mozliwosci na klucz WPS 2. Narysuj wymiane 4way handshake pomiedzy ap i stacja
Funkcje 4 way handshake do czego służy Pyrit czym jest
Co to jest GTK dlaczego tablice tęczowe przyspieszają łamanie

Grupa 1
○ Dlaczego WPA2 jest lepsze od WPA
WPA używa RC4, a WPA2 AES
○ Jak przechwycić 4 way handshake
To be able to successfully crack WPA-PSK password we need to capture an
initial authentication 4-way handshake. We can wait for a station connecting
to the targeted network but what to do if this is not happening? There is a way
to remote force a PC to reauthenticate. You can use aireplay-ng to
deauthenticate the station. Aireplay-ng sends a message to the Access Point
saying that the wireless client is no longer associated with the AP. The
wireless client will then hopefully reauthenticate with the AP. This generates
the 4-way handshake we are looking for
● Grupa 2
○ Dlaczego nie używać popularnych nazw SSID?
SSID jest używany jako sól do hashowania kluczy, a dla popularnych są
gotowe tablice tęczowe w sieci
○ Jakie wady ma WPS z PINem?
Access Point verifies the correctness of the PIN code in two steps. At the
beginning it checks the first 4 numbers ( variants) and after that it informs104
us we have the half of the PIN. Then the AP checks the second half (103
variants). Because of this approach, in the worst case we always have only 11
000 combinations of PIN code ( + variants). The 8th number of PIN104 103
code is a checksum of previous numbers.
● Grupa 3
○ Co jest ustalane podczas 4 way hadshake’u (wymień 2 elementy)
Group Temporal Key which is used to secure broadcasted messages.
PTK (Pairwise Transient Key)
○ Jak tablice tęczowe przyspieszają łamanie
Generating PMKs for the target network beforehand can speed up the
process of cracking the WPA/WPA2 key. The precomputed set of possible
PMKs hashes (MICs) is commonly called a rainbow table. As SSID is used to
salt passphrases, separate rainbow tables should be prepared for every
SSID.
● Grupa 4
○ WPS PBC - Push-Button-Connect, In this mode we don’t need any secret
passwords. The only thing we have to do is to press a button located on the
AP, and the client that is waiting for authentication will automatically connect.
When we turn on this mode, both AP and client scan the environment in
search of the other devices. After they detect each other, the authentication
process is similar to the PIN mode, but the code is by default 00000000.
○ jak łamać hasła WPA/WPA2
albo tablica tęczowa (z SSID mamy skróty haseł) ewentualnie atak siłowy