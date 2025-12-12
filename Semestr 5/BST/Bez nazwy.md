***1. WiFi: VAP vs. VLAN vs. VIF*** 
Te trzy akronimy współpracują ze sobą, ale działają na różnych poziomach: 

* ***VAP (Virtual Access Point):*** Warstwa radiowa. To wirtualne SSID (np. "Dom" i "Goście") nadawane z jednego fizycznego urządzenia. 

* ***VLAN (Virtual LAN):*** Warstwa sieciowa. Logiczna separacja ruchu (tagowanie pakietów), aby odizolować np. sieć gości od domowej. 

* ***VIF (Virtual Interface):*** Warstwa systemu operacyjnego. Reprezentacja interfejsu w jądrze systemu (np. `ath0`, `wl0.1`), która spina VAP z VLANem.

**2. iptables: Tabele, Łańcuchy i Cele*** 

Kluczowe elementy firewalla w Linuxie: 

* ***Tabela Filter:*** Służy do bezpieczeństwa. Łańcuchy: ***INPUT*** (do serwera), ***OUTPUT*** (z serwera), ***FORWARD*** (przez serwer/router). 
* ***Tabela NAT:*** Służy do translacji adresów. Łańcuchy: ***PREROUTING*** (DNAT - przekierowanie portów), ***POSTROUTING*** (SNAT/Maskarada - udostępnianie internetu). 
* ***Cele (Targets):*** Decydują o losie pakietu, np. ***ACCEPT*** (wpuść), ***DROP*** (usuń po cichu), ***REJECT*** (odrzuć z błędem), ***MASQUERADE*** (dynamiczne IP wyjściowe). 

 ***3. Port Triggering (Wyzwalanie Portów)*** 
 
* Dynamiczna alternatywa dla Port Forwardingu:
* ***Działanie:*** Ruch wychodzący na określonym porcie (***Trigger***) automatycznie otwiera inny port przychodzący (***Target***) dla tego konkretnego urządzenia. 
* ***Zalety:*** Bezpieczniejszy (porty są zamknięte, gdy nieużywane) i nie wymaga statycznego IP w sieci lokalnej. 
* ***Wada:*** Z reguły może korzystać tylko jedno urządzenie w danej chwili. 

***4. Obiekty `tc` (Traffic Control)**

Narzędzia do kształtowania ruchu (QoS) w Linuxie tworzą hierarchię: 

* ***QDisc (Queueing Discipline):*** Główny zarządca kolejki (korzeń), decyduje jak wysyłać pakiety (np. `pfifo_fast`, `htb`). 
* ***Class (Klasa):*** Występuje w **Classful QDiscs**. Pozwala dzielić pasmo na mniejsze kawałki (hierarchia, np. "ruch priorytetowy", "reszta"). 
* ***Filter (Filtr):*** Mechanizm klasyfikacji. Sprawdza nagłówki pakietów i kieruje je do odpowiedniej ***Klasy*** (np. filtr `u32` lub `fwmark`).