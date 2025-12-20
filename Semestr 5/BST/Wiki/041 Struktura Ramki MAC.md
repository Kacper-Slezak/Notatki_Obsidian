---
tags: [mac, ramka, nagłówek, bity]
---
# Struktura Ramki MAC 802.11

Ramka MAC jest znacznie bardziej skomplikowana niż w Ethernecie. Ma zmienną długość nagłówka.

## Ogólny Format Ramki (General Frame Format)
| Pole | Rozmiar | Opis |
| :--- | :---: | :--- |
| **Frame Control** | 2 bajty | Sterowanie (szczegóły poniżej). |
| **Duration / ID** | 2 bajty | Czas rezerwacji kanału (dla NAV) lub ID stacji (w PS-Poll). |
| **Address 1 (RA)** | 6 bajtów | Odbiorca (Receiver Address). Zawsze ten, kto ma odebrać fale radiowe. |
| **Address 2 (TA)** | 6 bajtów | Nadawca (Transmitter Address). Zawsze ten, kto wysyła fale. |
| **Address 3** | 6 bajtów | Zależy od ToDS/FromDS (często Destination lub Source). |
| **Sequence Control** | 2 bajty | Numer sekwencyjny i numer fragmentu. |
| **Address 4** | 6 bajtów | Tylko w trybie WDS (Bridge). |
| **Frame Body** | 0-2312 B | Dane (Payload). |
| **FCS (CRC)** | 4 bajty | Suma kontrolna (Cyclic Redundancy Check). |

---

## Pole Frame Control (2 Bajty) - Bit po bicie
Kluczowe pole decydujące o interpretacji ramki.

| Ver | Type | Subtype | To DS | From DS | More Frag | Retry | Pwr Mgt | More Data | WEP | Order |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| 2b | 2b | 4b | 1b | 1b | 1b | 1b | 1b | 1b | 1b | 1b |

1.  **Protocol Version:** Zawsze `00`.
2.  **Type & Subtype:** Określają funkcję ramki.
    * **Management (`00`):**
        * `1000` (8) = **Beacon**
        * `0100` (4) = **Probe Request**
        * `1011` (11) = **Authentication**
    * **Control (`01`):**
        * `1011` (11) = **RTS**
        * `1100` (12) = **CTS**
        * `1101` (13) = **ACK**
    * **Data (`10`):**
        * `0000` (0) = Zwykła ramka **Data**
        * `0100` (4) = **Null** (pusta ramka, np. do Power Management).



---

## Adresowanie (3 vs 4 Adresy)
Znaczenie pól adresowych zmienia się w zależności od bitów `To DS` i `From DS` w polu Frame Control.

| To DS | From DS | Sytuacja | Adres 1 (Odbiorca) | Adres 2 (Nadawca) | Adres 3 | Adres 4 |
| :---: | :---: | :--- | :--- | :--- | :--- | :--- |
| **0** | **0** | **Ad-hoc / Mgmt** | DA (Docelowy) | SA (Źródłowy) | BSSID | - |
| **0** | **1** | **Downlink (AP -> STA)** | DA (Stacja) | BSSID (AP) | SA (Źródłowy z sieci) | - |
| **1** | **0** | **Uplink (STA -> AP)** | BSSID (AP) | SA (Stacja) | DA (Docelowy w sieci) | - |
| **1** | **1** | **WDS (Most AP-AP)** | RA (Odbiorczy AP) | TA (Nadawczy AP) | DA | SA |

> [!tip] Jak zapamiętać?
> * **Adres 1** to ZAWSZE odbiorca radiowy (ten, co ma usłyszeć).
> * **Adres 2** to ZAWSZE nadawca radiowy (ten, co wysyła).
> * Jeśli wysyłasz do Internetu (Uplink, ToDS=1), to **Adres 1** to Twój AP (Bramka).