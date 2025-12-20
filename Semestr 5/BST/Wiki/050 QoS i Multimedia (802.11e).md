---
tags:
  - qos
  - 80211e
  - edca
  - hcca
  - multimedia
---
# Jakość Usług (QoS) - IEEE 802.11e

Standard 802.11e wprowadza mechanizm **HCF (Hybrid Coordination Function)**, który pozwala na priorytetyzację ruchu. Dzieli się on na dwie metody dostępu.

## 1. EDCA (Enhanced Distributed Channel Access)
Rozszerzenie podstawowego DCF. Zamiast jednej kolejki FIFO, mamy **4 Kategorie Dostępu (AC - Access Categories)**.

### Kategorie Dostępu (AC)
Mapowanie priorytetów z Ethernetu (802.1D - VLAN Tag) na Wi-Fi:

| AC (Kategoria) | Opis | Priorytet 802.1D | Zastosowanie |
| :--- | :--- | :---: | :--- |
| **AC_VO** (Voice) | Głos | 7, 6 | Najwyższy. VoIP, opóźnienia krytyczne. |
| **AC_VI** (Video) | Wideo | 5, 4 | Wysoki. Streaming, IPTV. |
| **AC_BE** (Best Effort)| Najlepsza staranność | 0, 3 | Średni. Internet, Web, Mail. |
| **AC_BK** (Background)| Tło | 2, 1 | Najniższy. Backupy, drukowanie. |

### Parametry różnicujące (EDCA Parameters)
Każda kategoria ma własny zestaw parametrów, co daje jej statystyczną przewagę:
1.  **AIFS (Arbitrary IFS):** Zamiast stałego DIFS. `AIFS[AC] = SIFS + AIFSN[AC] * Slot`.
    * *Dla Voice:* AIFSN = 2 (bardzo krótki czas oczekiwania).
    * *Dla Background:* AIFSN = 7 (długie czekanie).
2.  **CWmin / CWmax:** Okna rywalizacji.
    * *Dla Voice:* Małe okno (startuje szybciej).
    * *Dla Background:* Duże okno.
3.  **TXOP Limit (Transmission Opportunity):** Czas, przez który stacja może nadawać serię ramek bez ponownej rywalizacji (bursting).

## 2. HCCA (HCF Controlled Channel Access)
Rozszerzenie PCF (Polling). Wymaga centralnego zarządcy (**Hybrid Coordinator** w AP).
* Działa w oparciu o **TSPEC (Traffic Specification)**. Stacja negocjuje z AP: "Potrzebuję 1 Mbps i opóźnienie < 10ms".
* AP przydziela gwarantowane okna czasowe (TXOP) w fazie bezrywalizacyjnej.

## Dodatkowe Mechanizmy 802.11e
1.  **Block ACK:** Zamiast potwierdzać każdą ramkę osobno (co zajmuje czas SIFS+ACK), wysyłamy **jedno zbiorcze potwierdzenie** dla całej serii ramek (np. 64 ramek naraz). Zwiększa wydajność ("Throughput").
    * *Immediate Block ACK:* Potwierdzenie natychmiastowe.
    * *Delayed Block ACK:* Potwierdzenie w późniejszym czasie.
2.  **NoAck:** Tryb bez potwierdzeń. Używany dla ruchu, gdzie retransmisja nie ma sensu (np. VoIP w bardzo dobrej jakości - lepiej zgubić pakiet niż go opóźniać).
3.  **DLS (Direct Link Setup):** Pozwala stacjom w BSS przesyłać dane bezpośrednio między sobą (z pominięciem AP), ale pod kontrolą AP. Oszczędza pasmo (1 transmisja zamiast 2).