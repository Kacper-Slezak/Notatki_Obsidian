---
tags: [wykład, 802.11n, mimo, roaming, mesh, 802.11p]
alias: [Wykład 12 - Rozszerzenia i 802.11n]
---
# Wykład 12: IEEE 802.11 Część VII - High Throughput i Alfabet

## 1. Przegląd Rozszerzeń ("Zupa Literowa")

* **802.11j (Japan):** Praca w pasmach 4.9 GHz i 5 GHz w Japonii. Węższe kanały (10 MHz).
* **802.11k (Radio Resource Measurement):**
    * Klient pyta AP o statystyki kanału (Noise Histogram, Channel Load).
    * **Neighbor Report:** AP wysyła klientowi listę sąsiednich AP, co przyspiesza skanowanie przy roamingu (klient nie musi skanować wszystkich kanałów "w ciemno").
* **802.11p (WAVE - Wireless Access in Vehicular Environments):**
    * Pasmo: **5.9 GHz**.
    * Zastosowanie: Komunikacja między pojazdami (V2V) i infrastrukturą (V2I).
    * Cechy: Brak klasycznej asocjacji (tryb "Wildcard BSSID"), praca przy prędkościach do 200 km/h.
* **802.11r (Fast BSS Transition / Fast Roaming):**
    * Skraca czas przełączania (Handover) do **< 50 ms** (wymóg dla VoIP).
    * **Mechanizm:** Klucze szyfrujące (PTK) są negocjowane z nowym AP *zanim* klient się przełączy (Over-the-Air lub Over-the-DS). Eliminuje pełny 4-Way Handshake przy zmianie AP.
* **802.11s (Mesh Networking):**
    * Sieci kratowe. AP komunikują się ze sobą bezprzewodowo (tworząc WDS).
    * Protokół routingu w warstwie 2: **HWMP** (Hybrid Wireless Mesh Protocol).
* **802.11u:** Współpraca z sieciami zewnętrznymi (np. 3G/LTE). Podstawa **Hotspot 2.0** (Passpoint) - automatyczne logowanie karty SIM do Wi-Fi.
* **802.11v (Wireless Network Management):** Umożliwia AP sterowanie klientami (np. wymuszenie przejścia na inny AP - Load Balancing, zarządzanie czasem uśpienia - Max Idle Period).
* **802.11z (TDLS - Tunneled Direct Link Setup):** Umożliwia zestawienie bezpośredniego tunelu między dwoma klientami w tej samej sieci (z pominięciem AP dla danych), co odciąża AP.

---

## 2. IEEE 802.11n (High Throughput - Wi-Fi 4)
Standard wprowadzający rewolucyjne zmiany w warstwie fizycznej (MIMO).
* **Prędkość:** Do **600 Mbps** (przy 4x4 MIMO, 40 MHz).
* **Pasma:** 2.4 GHz i 5 GHz.

### Kluczowe Technologie 11n
1.  **MIMO (Multiple Input Multiple Output):**
    * **Spatial Multiplexing:** Wysyłanie różnych strumieni danych z różnych anten jednocześnie. Zwiększa przepustowość liniowo (2 anteny = 2x szybciej).
    * **Transmit Beamforming (TxBF):** Kształtowanie wiązki w stronę klienta (zwiększa zasięg/SNR).
2.  **Channel Bonding (40 MHz):**
    * Połączenie dwóch kanałów 20 MHz.
    * Podwaja liczbę podnośnych (z 52 do 108 dla danych).
3.  **Frame Aggregation (Agregacja):**
    * **A-MSDU:** Wiele pakietów IP w jednej ramce MAC.
    * **A-MPDU:** Wiele ramek MAC w jednej transmisji fizycznej. Zmniejsza narzut preambuły PHY i Backoffu.
4.  **Short Guard Interval (SGI):** Skrócenie przerwy między symbolami z 800 ns do **400 ns**. Zysk ~11%.