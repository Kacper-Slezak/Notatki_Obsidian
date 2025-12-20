---
tags: [mac, dcf, pcf, csma, backoff]
---
# Warstwa MAC - Metody Dostępu

Warstwa MAC w 802.11 odpowiada za sprawiedliwy dostęp do wspólnego medium radiowego.

## 1. DCF (Distributed Coordination Function)
Mechanizm obowiązkowy, oparty na rywalizacji (Contention-based).
* **Protokół:** **CSMA/CA** (Carrier Sense Multiple Access with Collision Avoidance). W przeciwieństwie do Ethernetu (CSMA/CD), tutaj **nie wykrywamy kolizji w trakcie nadawania**, staramy się ich unikać.

### Mechanizm Działania (Krok po kroku)
1.  **Nasłuch (Carrier Sense):**
    * **Fizyczny:** Sprawdzenie poziomu energii w antenie (CCA - Clear Channel Assessment).
    * **Wirtualny (NAV - Network Allocation Vector):** Licznik ustawiany na podstawie pola `Duration` w ramkach innych stacji. Jeśli NAV > 0, medium jest zajęte.
2.  **Oczekiwanie (IFS):** Jeśli medium wolne przez czas **DIFS**, stacja może nadawać (lub zacząć odliczanie).
3.  **Losowy Backoff (Odejmowanie):**
    * Stacja losuje liczbę szczelin czasowych (Slot Time) z przedziału `[0, CW]`.
    * Licznik zmniejsza się, gdy kanał jest wolny.
    * Licznik "zamarza", gdy ktoś inny zaczyna nadawać.
    * Gdy licznik dojdzie do 0 -> **Transmisja**.

> [!important] Procedura Backoff (Binary Exponential Backoff)
> * **CW (Contention Window):** Okno rywalizacji.
> * Startujemy z `CWmin` (np. 15 lub 31).
> * Po każdej nieudanej transmisji (brak ACK), `CW` jest podwajane: `CW_new = 2 * (CW_old + 1) - 1`.
> * Rośnie aż do `CWmax` (np. 1023).
> * Po udanym ACK, wracamy do `CWmin`.

## 2. PCF (Point Coordination Function)
Mechanizm opcjonalny, bezrywalizacyjny (Contention-free).
* AP działa jako **Point Coordinator (PC)**.
* **Polling:** AP wysyła zapytanie (CF-Poll) do konkretnej stacji: "Czy masz coś do wysłania?". Stacja odpowiada od razu (po czasie SIFS).
* Gwarantuje pasmo (dobre dla Voice/Video), ale jest mało efektywne przy małym ruchu.

## 3. Odstępy Międzyramkowe (IFS - Interframe Spaces)
Czas ciszy między ramkami wyznacza priorytet. **Krótszy czas = Wyższy priorytet**.

| Typ IFS | Czas (przykład 802.11b) | Zastosowanie / Priorytet |
| :--- | :--- | :--- |
| **SIFS** (Short) | 10 µs | **Najwyższy.** ACK, CTS, Fragmenty. Pozwala "wcisnąć się" w rozmowę. |
| **PIFS** (PCF) | SIFS + Slot (30 µs) | Średni. Używany przez AP w trybie PCF do przejęcia kanału. |
| **DIFS** (DCF) | SIFS + 2*Slot (50 µs) | **Niski.** Standardowy dostęp dla danych w DCF. |
| **EIFS** (Extended) | Zmienny (Długi) | Najniższy. Używany po odebraniu **błędnej ramki** (CRC Error), żeby dać czas na wysłanie ACK przez kogoś innego. |