---
tags:
  - osi
  - tcp
  - udp
---

Podstawą komunikacji jest **enkapsulacja** danych. Każda warstwa dodaje własny nagłówek (Header).

### Porównanie Modeli

|Warstwa (OSI)|Odpowiednik TCP/IP|Protokół / Jednostka|Przykład / Funkcja|
|---|---|---|---|
|**Aplikacji**|Aplikacja|**Data** (Dane)|HTTP, DNS, SSH, MQTT|
|**Transportowa**|Transport|**Segment** (TCP) / **Datagram** (UDP)|Porty (0-65535), Niezawodność|
|**Sieciowa**|Internet|**Packet** (Pakiet)|IP, ICMP, Routing|
|**Łącza danych**|Dostęp do sieci|**Frame** (Ramka)|Adresy MAC, Ethernet, Wi-Fi|
### Szczegóły Warstwy Transportowej

- **TCP (3-way Handshake):** 1. `SYN` (Klient) -> 2. `SYN-ACK` (Serwer) -> 3. `ACK` (Klient).
    
    - _Kluczowe:_ Zapewnia kolejność pakietów i retransmisję.
        
- **UDP:** Bezpołączeniowy. Brak gwarancji dostarczenia, ale minimalny overhead. Wykorzystywany przez [[#Protokół QUIC|QUIC]].