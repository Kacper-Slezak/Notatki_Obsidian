---
tags:
  - csma
---

**1. Mechanizm Backoff i okno rywalizacji (CW):**

- **Procedura:** Stacja po wykryciu wolnego medium (DIFS) losuje liczbę szczelin czasowych (Slot Time) z przedziału [0,CW]. Jeśli medium jest zajęte, licznik zostaje wstrzymany i wznowiony dopiero po czasie DIFS bezczynności kanału.
    
- **Binary Exponential Backoff:** W przypadku kolizji (braku ramki ACK), wartość CWmin​ jest podwajana (2n−1) aż do osiągnięcia CWmax​. Po udanej transmisji wartość wraca do CWmin​.
    
- **Rola CWmax:** Zapobiega niekontrolowanemu wzrostowi opóźnień, ale musi być wystarczająco duża (np. 8191), aby rozproszyć stacje w czasie przy dużym obciążeniu (nasyceniu).
    

**2. Analiza wydajności (Wnioski z symulacji):**

- **Wpływ długości ramki:** Sieć wykazuje bardzo niską wydajność przy krótkich ramkach danych. Wynika to z faktu, że narzut (overhead) – czyli czasy DIFS, SIFS, preambuła fizyczna (PLCP) oraz ramka ACK – jest stały. Przy krótkich danych narzut ten dominuje nad czasem samej transmisji danych.
    
- **Liczba stacji a nasycenie:** Wraz ze wzrostem liczby stacji w warunkach nasycenia, drastycznie rośnie liczba kolizji, co obniża sumaryczną przepustowość. Optymalna wartość CWmin​ zależy od liczby aktywnych stacji – dla 100 stacji wymagane jest znacznie większe okno początkowe niż dla 5.
    

**Powiązania:**

- [[040 Warstwa MAC i Dostęp (DCF, PCF)]] - Szczegóły CSMA/CA.
    
- [[010 Wstęp i Pasma Radiowe]] - Charakterystyka medium radiowego.