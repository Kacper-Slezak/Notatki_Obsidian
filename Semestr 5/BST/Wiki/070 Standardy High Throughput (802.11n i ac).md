---
tags: [standardy, wifi4, wifi5, mimo, bonding]
---
# High Throughput (Wi-Fi 4 & 5)

## 1. IEEE 802.11n (Wi-Fi 4) - High Throughput
Standard, który zmienił wszystko w 2009 roku.
* **Pasma:** Działa zarówno w **2.4 GHz**, jak i **5 GHz**.
* **Maksymalna prędkość:** do **600 Mbps** (przy 4 antenach i kanale 40 MHz).

### Kluczowe Technologie 11n
1.  **MIMO (Multiple Input Multiple Output):**
    * Wykorzystuje zjawisko wielodrogowości (odbicia sygnału), które wcześniej było problemem.
    * **Spatial Multiplexing (SDM):** Przesyłanie niezależnych strumieni danych różnymi antenami (np. 2x2 = podwojenie prędkości).
    * **STBC (Space-Time Block Coding):** Zwiększenie zasięgu poprzez wysyłanie tych samych danych (zakodowanych) na wielu antenach.
2.  **Channel Bonding (40 MHz):**
    * Połączenie dwóch kanałów 20 MHz.
    * Zysk ponad 2x (bo usuwamy pasmo ochronne między kanałami).
3.  **Frame Aggregation (Agregacja Ramek):**
    * Zamiast wysyłać małe ramki z dużym narzutem nagłówka PHY, łączymy je.
    * **A-MSDU:** Łączenie pakietów IP w jedną ramkę MAC (jeden nagłówek MAC).
    * **A-MPDU:** Łączenie ramek MAC w jedną dużą transmisję fizyczną (wspólny nagłówek PHY, ale osobne sumy kontrolne CRC). Bardziej odporne na błędy.
4.  **Guard Interval (GI):**
    * Standardowy GI = 800 ns.
    * **Short GI = 400 ns.** Zysk ~10% przepustowości.

## 2. IEEE 802.11ac (Wi-Fi 5) - Very High Throughput
Ewolucja skupiona na prędkości.
* **Pasmo:** Tylko **5 GHz**.
* **Modulacja:** **256-QAM** (8 bitów na symbol). Wymaga bardzo silnego sygnału (blisko AP).
* **Szersze kanały:** **80 MHz** (obowiązkowe) i **160 MHz** (opcjonalne, rzadko używane w praktyce przez zakłócenia).
* **DL MU-MIMO (Downlink Multi-User MIMO):**
    * AP może nadawać do kilku klientów (max 4) **jednocześnie**.
    * Wymaga precyzyjnego **Beamformingu** (formowania wiązki).****