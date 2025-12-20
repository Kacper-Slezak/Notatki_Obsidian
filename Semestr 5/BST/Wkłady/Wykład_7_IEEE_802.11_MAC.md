---
tags: [wykład, mac, csma, dcf, pcf, ramki]
alias: [Wykład 7 - Warstwa MAC]
---
# Wykład 7: IEEE 802.11 Część II - Warstwa MAC i Dostęp

## 1. Specyfika Medium Bezprzewodowego
W przeciwieństwie do Ethernetu (kabel), w radiu nie można łatwo wykryć kolizji w trakcie nadawania, ponieważ własny sygnał zagłusza wszystko inne (problem Near-Far).
* **Ethernet:** CSMA/CD (Collision Detection).
* **Wi-Fi:** **CSMA/CA** (Collision Avoidance).

## 2. Metody Dostępu (Coordination Functions)
Standard definiuje dwa tryby dostępu:

### A. DCF (Distributed Coordination Function) - Obowiązkowy
Oparty na rywalizacji. Każda stacja walczy o dostęp.
1.  **Carrier Sense (Nasłuch):**
    * **Fizyczny:** Sprawdza energię w antenie (CCA).
    * **Wirtualny (NAV):** Licznik odczytywany z pola `Duration` w ramkach innych stacji. Jeśli NAV > 0, czekamy.
2.  **IFS (Inter Frame Space):** Obowiązkowa cisza między ramkami.
3.  **Backoff (Losowe opóźnienie):**
    * Jeśli kanał zajęty -> wylosuj czas z przedziału `[0, CW]`.
    * Zmniejszaj licznik tylko, gdy kanał wolny.
    * Gdy licznik = 0 -> Nadawaj.

> [!algorithm] Binary Exponential Backoff
> Po każdej kolizji (brak ACK), okno rywalizacji (**CW**) jest podwajane (`CW_new = 2 * (CW + 1) - 1`) aż do `CWmax`. Po sukcesie wraca do `CWmin`.

### B. PCF (Point Coordination Function) - Opcjonalny
Tryb bezrywalizacyjny, sterowany przez AP (Point Coordinator).
* AP odpytuje stacje (**Polling**) czy mają dane.
* Gwarantuje dostęp (dobre dla Voice/Video), ale mało efektywne w tłoku.
* Działa w okresie CFP (Contention Free Period).

---

## 3. Priorytetyzacja (Interwały IFS)
Czas oczekiwania na wolne medium decyduje o priorytecie. Krótszy czas = szybszy dostęp.

| Nazwa | Skrót | Czas (DSSS) | Zastosowanie |
| :--- | :--- | :--- | :--- |
| **Short IFS** | **SIFS** | 10 µs | **Najwyższy.** ACK, CTS, Fragmenty. Pozwala dokończyć trwającą wymianę. |
| **PCF IFS** | **PIFS** | SIFS + Slot (30 µs) | Średni. Używany przez AP w trybie PCF. |
| **DCF IFS** | **DIFS** | SIFS + 2*Slot (50 µs) | **Niski.** Standardowy dostęp dla danych (DCF). |
| **Extended IFS**| **EIFS** | Zmienny | Najniższy. Używany po wykryciu błędu transmisji (CRC Error). |

---

## 4. Mechanizmy Ochrony i Wydajności

### RTS/CTS (Rozwiązanie problemu ukrytej stacji)
Stacja A i C mogą się nie słyszeć, ale obie nadają do B -> Kolizja u B.
1.  Nadawca wysyła **RTS (Request to Send)** z czasem trwania.
2.  Odbiorca (jeśli wolny) odsyła **CTS (Clear to Send)**.
3.  Wszyscy, którzy słyszą CTS (nawet jak nie słyszeli RTS), ustawiają **NAV** i milkną.
4.  Dane są wysyłane.

### Fragmentacja
Duże ramki są bardziej podatne na błędy.
* Dzielimy MSDU na mniejsze fragmenty.
* Każdy fragment ma własne CRC i wymaga osobnego ACK (ACK odsyłany po SIFS).
* W przypadku błędu, retransmitujemy tylko uszkodzony fragment.

---

## 5. Struktura Ramki MAC
Ramka MAC jest skomplikowana. Najważniejszy jest nagłówek.

### Pole Frame Control (2 bajty)
Decyduje o typie ramki.
* **Protocol Ver:** Zawsze `00`.
* **Type (2b) & Subtype (4b):**
    * `00` **Management:** Beacon, Probe Req/Resp, Auth, Assoc.
    * `01` **Control:** RTS, CTS, ACK, PS-Poll.
    * `10` **Data:** Zwykłe dane.
* **To DS / From DS:** (Kluczowe dla adresowania - patrz niżej).
* **More Frag:** 1 = to nie jest ostatni fragment.
* **Retry:** 1 = to jest retransmisja.
* **Pwr Mgt:** 1 = stacja przechodzi w tryb uśpienia po tej ramce.
* **WEP:** 1 = dane są zaszyfrowane.

### Adresowanie (Pola Address 1-4)
Znaczenie pól zależy od kierunku ruchu.

| To DS | From DS | Scenariusz | Adres 1 (Odbiorca radiowy) | Adres 2 (Nadawca radiowy) | Adres 3 | Adres 4 |
| :---: | :---: | :--- | :--- | :--- | :--- | :--- |
| 0 | 0 | **Ad-hoc / Mgmt** | DA (Docelowy) | SA (Źródłowy) | BSSID | - |
| 0 | 1 | **Downlink (od AP)**| DA (Stacja) | BSSID (AP) | SA (Oryginalny nadawca) | - |
| 1 | 0 | **Uplink (do AP)** | BSSID (AP) | SA (Stacja) | DA (Oryginalny cel) | - |
| 1 | 1 | **WDS (Bridge)** | RA (Odbiorczy AP)| TA (Nadawczy AP)| DA | SA |

> [!tip] Reguła
> * **Addr 1** to zawsze ten, kto ma **odebrać** sygnał radiowy.
> * **Addr 2** to zawsze ten, kto **wysłał** sygnał radiowy.
