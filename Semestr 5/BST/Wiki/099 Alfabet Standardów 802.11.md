---
tags: [standardy, lista, definicje]
---
# Alfabet Standardów IEEE 802.11

Kompletna lista rozszerzeń standardu.

## Główne Standardy (Warstwa Fizyczna)
| Std          | Pasmo   | Max Prędkość | Modulacja     | Kluczowa Cecha                      |
| :----------- | :------ | :----------- | :------------ | :---------------------------------- |
| **802.11**   | 2.4     | 2 Mbps       | DSSS/FHSS     | Legacy                              |
| **802.11b**  | 2.4     | 11 Mbps      | HR-DSSS (CCK) | Pierwszy popularny Wi-Fi            |
| **802.11a**  | 5       | 54 Mbps      | OFDM          | Wprowadzenie OFDM                   |
| **802.11g**  | 2.4     | 54 Mbps      | ERP-OFDM      | Kompatybilność z 'b' + prędkość 'a' |
| **802.11n**  | 2.4/5   | 600 Mbps     | HT-OFDM       | **MIMO**, Kanał 40MHz, Aggregation  |
| **802.11ac** | 5       | 6.9 Gbps     | VHT-OFDM      | **MU-MIMO (DL)**, 160MHz, 256-QAM   |
| **802.11ax** | 2.4/5/6 | 9.6 Gbps     | HE-OFDMA      | **OFDMA**, 1024-QAM, BSS Color      |
| **802.11ad** | 6       | 7 Gbps       | SC/OFDM       | **WiGig**, krótki zasięg (pokój)    |

## Rozszerzenia Funkcjonalne (Literki)
* **802.11c:** Procedury pracy mostu (Bridge Operation). Kluczowe dla konstrukcji AP.
* **802.11d:** "World Mode". Rozgłaszanie kodu kraju i dopuszczalnych kanałów w ramkach Beacon.
* **802.11e:** **QoS (Quality of Service)**. Wprowadza priorytety (TXOP, AIFS) i mechanizm HCF (EDCA/HCCA).
* **802.11f:** IAPP (Inter-Access Point Protocol). Protokół wymiany informacji między AP (wycofany, zastąpiony przez 11r).
* **802.11h:** Zarządzanie widmem 5 GHz w Europie (**DFS** i **TPC**).
* **802.11i:** **Bezpieczeństwo (WPA2)**. Szyfrowanie AES-CCMP, autoryzacja 802.1X.
* **802.11j:** Rozszerzenie dla pasma 4.9/5 GHz w Japonii.
* **802.11k:** Pomiary radiowe (**Radio Resource Measurement**). Klient raportuje stan kanału, ułatwia roaming.
* **802.11m:** Maintenance (konserwacja dokumentacji standardu).
* **802.11p:** **WAVE (Vehicular)**. Komunikacja samochodów (V2X) w paśmie 5.9 GHz.
* **802.11r:** **Fast Roaming** (Fast BSS Transition). Przełączanie < 50ms (dla VoIP).
* **802.11s:** **Mesh**. Sieci kratowe, routing HWMP.
* **802.11T:** (WIP) Wireless Performance Prediction (testowanie wydajności).
* **802.11u:** Interworking z sieciami zewnętrznymi (np. 3G/GSM). Podstawa Hotspot 2.0 (Passpoint).
* **802.11v:** Zarządzanie siecią (**Wireless Network Management**). Load balancing, oszczędzanie energii, sterowanie klientem.
* **802.11w:** Ochrona ramek zarządzających (**Protected Management Frames**). Chroni przed atakami Deauth/Disassoc.
* **802.11y:** Praca w paśmie licencjonowanym 3.65-3.7 GHz (USA). Duża moc.
* **802.11z:** **TDLS** (Tunneled Direct Link Setup). Bezpośrednie połączenie stacja-stacja wewnątrz BSS.
* **802.11aa:** Ulepszenia Video/Audio (Reliability, Multicast).
* **802.11af:** **White-Fi**. Praca w pasmach TV (VHF/UHF). Duży zasięg.
* **802.11ah:** **HaLow**. Pasmo < 1 GHz (Sub-1GHz) dla IoT.
* **802.11ai:** FILS (Fast Initial Link Setup). Bardzo szybkie łączenie (<100ms).
* **802.11aj:** "China Millimeter Wave". Odpowiednik 11ad dla Chin (45 GHz).
* **802.11aq:** Pre-association Discovery (znajdowanie usług przed połączeniem).