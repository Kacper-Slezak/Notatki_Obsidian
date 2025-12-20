---
tags: [wstęp, pasma, ISM, unii]
---
# Wstęp i Pasma Radiowe

## Zalety i Wyzwania WLAN

> [!info] Kluczowe Cechy
> * **Mobilność:** Brak kabla, swoboda ruchu.
> * **Elastyczność:** Pokrycie trudnych miejsc (zabytki), sieci Ad-hoc.
> * **Koszt:** Niskie koszty instalacji (brak kucia ścian), ale wyższe koszty urządzeń końcowych w porównaniu do prostego Ethernetu.
> * **Niezawodność:** Odporność na katastrofy fizyczne (np. trzęsienia ziemi).

## Pasma Radiowe (ISM vs UNII)
WLAN korzysta z pasm nielicencjonowanych.

### Pasmo 2.4 GHz (ISM - Industrial, Scientific, Medical)
* **Zakres:** 2.400 - 2.4835 GHz.
* **Kanały:**
    * Szerokość kanału: zazwyczaj **20/22 MHz**.
    * Odstęp między środkami kanałów: **5 MHz**.
    * **Wzór:** $F_c = 2407 + 5 \cdot k$ (MHz), dla $k=1...13$. (Kanał 14 jest wyjątkiem w Japonii).
    * **Kanały niepokrywające się (Non-overlapping):** Tylko **1, 6, 11** (w USA/Europie).
* **Wady:** Zatłoczenie (mikrofalówki, Bluetooth, ZigBee), mało miejsca na szerokie kanały.

### Pasmo 5 GHz (U-NII - Unlicensed National Information Infrastructure)
Podzielone na podzakresy (szczegóły ważne na egzamin):
1.  **U-NII-1 (Low):** 5.15 - 5.25 GHz (Indoor use only, max 40-50mW).
2.  **U-NII-2 (Mid):** 5.25 - 5.35 GHz (Wymaga **DFS** i **TPC**).
3.  **U-NII-2e (Extended):** 5.47 - 5.725 GHz (Wymaga DFS/TPC, outdoor).
4.  **U-NII-3 (Upper):** 5.725 - 5.825 GHz (Często używane w mostach radiowych).

> [!warning] Wymogi dla 5 GHz (Europa/Polska)
> Standard **802.11h** wymusza:
> * **DFS (Dynamic Frequency Selection):** Nasłuch radarów. Wykrycie radaru = zmiana kanału.
> * **TPC (Transmit Power Control):** Ograniczenie mocy do minimum niezbędnego do połączenia.

---