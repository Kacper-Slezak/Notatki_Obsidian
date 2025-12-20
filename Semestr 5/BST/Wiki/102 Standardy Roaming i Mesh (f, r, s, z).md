---
tags: [roaming, mesh, topologia]
---
# Roaming, Mesh i Połączenia Bezpośrednie

### 802.11f - IAPP (Inter-Access Point Protocol)
* [cite_start]**Status:** Wycofany (zastąpiony przez 802.11r)[cite: 1969].
* **Cel:** Pozwalał AP wymieniać się informacjami o użytkowniku podczas roamingu (przekazywanie kontekstu). Działał po Ethernecie (UDP/TCP).

### 802.11r - Fast BSS Transition (Fast Roaming)
* [cite_start]**Kluczowe słowo:** **< 50ms**[cite: 420].
* **Cel:** Szybkie przełączanie się między AP bez zrywania rozmów VoIP.
* **Jak:** Klucz szyfrowania jest negocjowany z nowym AP *zanim* klient się do niego przełączy (Fast Handshake).

### 802.11s - Mesh Networking
* [cite_start]**Co to:** Sieci kratowe[cite: 422].
* **Architektura:** AP łączą się ze sobą bezprzewodowo (jako routery), tworząc siatkę. Tylko jeden AP musi mieć kabel do Internetu (Mesh Portal).
* **Protokół:** HWMP (Hybrid Wireless Mesh Protocol).

### 802.11z - TDLS (Tunneled Direct Link Setup)
* [cite_start]**Co to:** Bezpośredni link tunelowany[cite: 447].
* **Działanie:** Jeśli dwa laptopy są w tej samej sieci WiFi, mogą przesyłać dane **bezpośrednio między sobą** (z pominięciem AP), ale nadal będąc podłączonym do AP. Odciąża to Access Point.