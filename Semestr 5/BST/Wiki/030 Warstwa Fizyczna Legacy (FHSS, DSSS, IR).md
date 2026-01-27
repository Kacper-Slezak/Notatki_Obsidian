---
tags: [phy, modulacja, legacy, fhss, dsss]
---
# Warstwa Fizyczna (PHY) - Technologie Legacy

Pierwsza wersja standardu (1997) definiowała trzy media transmisyjne. Wszystkie zapewniały 1 lub 2 Mbps.

## 1. Podczerwień (Infrared - IR)
* Praktycznie nieużywana.
* **Zasięg:** ok. 10m, wymaga odbić (diffuse light), nie przenika przez ściany.
* **Modulacja:** **PPM (Pulse Position Modulation)**.
    * **4-PPM** dla 2 Mbps (2 bity na symbol).
    * **16-PPM** dla 1 Mbps (4 bity na symbol).

## 2. FHSS (Frequency Hopping Spread Spectrum)
* **Zasada:** Sygnał "skacze" po wąskich kanałach w losowej sekwencji.
* **Pasmo:** 2.4 GHz podzielone na **2- 79 kanałów** o szerokości **1 MHz**.
* **Modulacja:**
    * **2-GFSK** (Gaussian FSK) dla 1 Mbps.
    * **4-GFSK** dla 2 Mbps.
* **Zalety:** Bardzo duża odporność na zakłócenia wąskopasmowe.
* **Parametry:**
    * **Dwell Time:** Czas przebywania na kanale (np. 390 ms).
    * **Hop Time:** Czas przeskoku.
* *Ciekawostka:* Bluetooth używa FHSS, ale skacze szybciej (1600 razy/s).

## 3. DSSS (Direct Sequence Spread Spectrum)
* **Zasada:** Każdy bit danych jest mnożony przez sekwencję rozpraszającą.
* **Kod Barkera (Barker Code):**
    * Sekwencja **11-bitowa**: `+1, -1, +1, +1, -1, +1, +1, +1, -1, -1, -1`.
    * Służy do rozpraszania widma i zwiększania odporności na zakłócenia (Gain).
* **Pasmo:** Kanał zajmuje ok. **22 MHz**.
* **Modulacja:**
    * **DBPSK** (Differential BPSK) -> 1 Mbps.
    * **DQPSK** (Differential QPSK) -> 2 Mbps.

> [!summary] Ewolucja w 802.11b (HR-DSSS)
> Aby uzyskać 5.5 i 11 Mbps (standard 'b'), porzucono Kod Barkera na rzecz **CCK (Complementary Code Keying)**.
> * Nadal zajmuje 22 MHz.
> * CCK koduje 4 lub 8 bitów na symbol.