---
tags:
  - wykład
  - 80211ac
  - 80211ax
  - wifi6
  - ofdma
  - mu-mimo
alias:
  - Wykład 13 - Wi-Fi 5 i Wi-Fi 6
---
# Wykład 13: IEEE 802.11 Część VIII - Gigabitowe Wi-Fi (ac/ax)

## 1. IEEE 802.11ac (VHT - Wi-Fi 5)
Ewolucja standardu 'n', działająca **wyłącznie w 5 GHz**.
* **Prędkość:** Do 6.9 Gbps (teoretycznie).
* **Szerokość kanału:** 80 MHz (obowiązkowe), **160 MHz** (opcjonalne, często jako 80+80 MHz).
* **Modulacja:** **256-QAM** (koduje 8 bitów na symbol). Wymaga bardzo wysokiego SNR.
* **DL MU-MIMO (Downlink Multi-User MIMO):**
    * AP może wysyłać dane do max 4 użytkowników jednocześnie.
    * Wymaga, aby użytkownicy byli przestrzennie odseparowani (aby wiązki się nie zakłócały).

## 2. Inne standardy specjalistyczne
* **802.11ad (WiGig):** Pasmo **60 GHz**. Zasięg pokojowy (nie przenika ścian), ale prędkości do 7 Gbps. Idealne do bezprzewodowego VR/HDMI.
* **802.11af (White-Fi):** Pasmo TV (VHF/UHF). Bardzo duży zasięg (kilometry), przenikanie przez przeszkody. Wykorzystuje "Białe Plamy" w widmie TV (Cognitive Radio).
* **802.11ah (HaLow):** Pasmo **Sub-1GHz** (np. 900 MHz). Dla IoT. Niski pobór mocy, duży zasięg, obsługa tysięcy sensorów przez jeden AP.
* **802.11ai (FILS):** Szybkie zestawianie połączenia (< 100ms). Optymalizacja skanowania i uwierzytelniania.

---

## 3. IEEE 802.11ax (HE - High Efficiency - Wi-Fi 6)
Najnowszy standard omawiany na wykładzie. Skupia się na **wydajności w gęstym środowisku** (High Density), a nie tylko na prędkości szczytowej.
* **Pasma:** 2.4 GHz i 5 GHz (oraz 6 GHz jako Wi-Fi 6E).

### Rewolucja: OFDMA (Orthogonal Frequency Division Multiple Access)
* **Problem:** W OFDM (11a/g/n/ac) jeden użytkownik zajmował cały kanał, nawet dla małego pakietu.
* **Rozwiązanie:** OFDMA dzieli kanał na **RU (Resource Units)**.
    * Kanał 20 MHz można podzielić na max 9 użytkowników (RU 26-tonowe).
    * AP przydziela podnośne konkretnym użytkownikom w każdej ramce.
    * Działa w **Downlink** i **Uplink**.

### Kluczowe Usprawnienia 11ax
1.  **1024-QAM:** Koduje 10 bitów na symbol. 25% wzrostu prędkości względem 256-QAM.
2.  **Uplink MU-MIMO:** Wiele stacji może jednocześnie nadawać do AP (w 11ac było tylko Downlink).
3.  **Dłuższy Symbol OFDM:** Wydłużony 4x (z 3.2 µs do **12.8 µs**). Zwiększa odporność na echa (Multipath) w środowisku outdoor.
4.  **BSS Coloring:**
    * 6 bitów w nagłówku PHY oznacza "kolor" sieci (BSS).
    * Pozwala ignorować transmisje sąsiednich sieci (OBSS - Overlapping BSS) i nadawać jednocześnie (Spatial Reuse), jeśli sygnał sąsiada jest słaby.
5.  **TWT (Target Wake Time):** AP i klient negocjują harmonogram wybudzeń. Idealne dla IoT (urządzenie może spać godzinami).