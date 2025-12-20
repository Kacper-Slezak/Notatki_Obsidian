---
tags:
  - wykład
  - qos
  - 80211e
  - edca
  - adaptacja
  - rate-control
alias:
  - Wykład 9 - QoS i Adaptacja
---
# Wykład 9: IEEE 802.11 Część IV - QoS i Adaptacja Prędkości

## 1. Adaptacja Prędkości (Dynamic Rate Adaptation)
Wi-Fi automatycznie zmienia prędkość (modulację) w zależności od jakości sygnału.
Jest to mechanizm sterownika, nie narzucony sztywno przez standard.

### Algorytmy Adaptacji
1.  **ARF (Auto Rate Fallback):**
    * Najprostszy. Dwa braki ACK pod rząd -> Zmniejsz prędkość.
    * 10 udanych transmisji (lub timer) -> Spróbuj zwiększyć prędkość (Probe).
    * *Wada:* Przy dużym tłoku (kolizje) błędnie uznaje, że sygnał jest słaby i zmniejsza prędkość, co tylko pogarsza sytuację (dłuższe ramki).
2.  **AARF (Adaptive ARF):** Ulepszony ARF. Jeśli próba zwiększenia prędkości się nie udała, wydłuża czas do kolejnej próby (Exponential Backoff dla próbkowania).
3.  **RRAA (Robust Rate Adaptation Algorithm):**
    * Używa statystyki strat (Loss Ratio) w oknie czasowym (Estimation Window).
    * Lepiej radzi sobie z odróżnianiem kolizji od słabego sygnału (dzięki użyciu RTS do sondowania).

### Anomalia Wydajności (Performance Anomaly)
W sieci z mieszanymi stacjami (szybkie 54 Mbps i wolne 1 Mbps), mechanizm CSMA/CA daje każdej stacji **równe prawdopodobieństwo** dostępu do medium, a nie równy *czas*.
* Wolna stacja zajmuje kanał przez bardzo długi czas, przesyłając mało danych.
* Efekt: Przepustowość całej sieci spada do poziomu najwolniejszego klienta.
* Rozwiązanie: **Airtime Fairness** (przydzielanie czasu antenowego, a nie liczby ramek) - mechanizm stosowany w nowoczesnych AP.

---

## 2. IEEE 802.11e - Jakość Usług (QoS)
Standard wprowadzający mechanizm **HCF (Hybrid Coordination Function)**.

### EDCA (Enhanced Distributed Channel Access)
Rozszerzenie DCF dla ruchu priorytetowego. Wprowadza 4 kolejki sprzętowe (**AC - Access Categories**):

| Kategoria (AC) | Typ ruchu | Priorytet | Parametry (AIFS, CW) |
| :--- | :--- | :--- | :--- |
| **AC_VO** | Voice (VoIP) | Najwyższy | Najkrótszy AIFS, Małe CWmin |
| **AC_VI** | Video | Wysoki | Krótki AIFS |
| **AC_BE** | Best Effort | Średni | Standardowe (jak DCF) |
| **AC_BK** | Background | Niski | Długi AIFS, Duże CWmin |

> [!important] TXOP (Transmission Opportunity)
> W standardowym DCF stacja może wysłać jedną ramkę. W 802.11e stacja, która wygrała dostęp (wygrała Backoff), otrzymuje prawo do nadawania przez czas **TXOP Limit**. Może wtedy wysłać serię ramek bez ponownej rywalizacji.

### HCCA (HCF Controlled Channel Access)
Wersja z centralnym sterowaniem (jak PCF, ale lepsza).
* AP (Hybrid Coordinator) negocjuje ze stacją parametry (**TSPEC**): "Gwarantuję Ci 2 Mbps pasma".
* AP wysyła ramki *QoS CF-Poll* w okresach wolnych od rywalizacji.

### Nowe mechanizmy wydajności
* **Block ACK:** Potwierdzanie wielu ramek jednym bitem w mapie bitowej (zamiast osobnych ACK).
* **NoAck:** Opcja wysyłania bez potwierdzeń (dla streamingu, gdzie opóźnienie retransmisji jest gorsze niż utrata piksela).
* **DLS (Direct Link Setup):** Pozwala na transmisję stacja-stacja z pominięciem AP (oszczędza pasmo radiowe o 50%).

---

## 3. Inne standardy z tego okresu
W agendzie tego wykładu często omawiane są też "małe literki":
* **802.11c:** Procedury mostkowania (Bridge).
* **802.11d:** World Mode (dostosowanie do przepisów radiowych w różnych krajach).
* **802.11f:** IAPP (Inter-Access Point Protocol) - wycofany, miał pomagać w roamingu.
* **802.11g:** Następca 802.11b w paśmie 2.4 GHz (wprowadził OFDM i 54 Mbps).