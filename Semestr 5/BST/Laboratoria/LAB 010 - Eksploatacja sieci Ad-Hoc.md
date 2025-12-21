---
tags:
  - adhoc
  - csma
  - ibss
---


**1. Charakterystyka IBSS (Independent BSS):**

- Brak centralnego AP. Wszystkie stacje są równe i odpowiedzialne za synchronizację (rozproszony mechanizm TSF) oraz rozgłaszanie ramek Beacon.
    
- **Ograniczenia:** Słabe zarządzanie energią (stacje muszą być częściej wybudzone), trudna skalowalność.
    

**2. Zjawisko Performance Anomaly:**

- **Problem:** W sieci Ad-Hoc (lub infrastrukturze), jeśli jedna stacja transmituje z niską prędkością (np. 1 Mbps - standard 'b'), drastycznie obniża to przepustowość stacji szybkich (np. 54 Mbps - standard 'g').
    
- **Przyczyna:** CSMA/CA zapewnia każdemu "sprawiedliwy" dostęp do wysłania ramki. Wolna stacja potrzebuje jednak 54 razy więcej czasu na przesłanie tej samej ilości danych, co blokuje medium dla innych.
    
- **Rozwiązanie:** Wprowadzenie mechanizmów sprawiedliwości czasowej (Airtime Fairness) zamiast sprawiedliwości ramkowej.
    

**Powiązania:**

- [[100 Standardy Podstawowe (a, b, g, n, ac, ax)]] - Sekcja o anomalii.
    
- [[040 Warstwa MAC i Dostęp (DCF, PCF)]] - Zasady rywalizacji o medium.