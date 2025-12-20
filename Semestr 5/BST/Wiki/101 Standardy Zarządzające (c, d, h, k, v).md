---
tags: [standardy, zarządzanie, regulacje]
---
# Standardy Zarządzające i Regulacyjne

Te standardy nie zwiększają prędkości, ale "naprawiają" działanie sieci.

### 802.11c - Bridge Operation
* [cite_start]**Co to:** Procedury operacyjne mostu (Bridge)[cite: 1745].
* **Cel:** Pozwala Access Pointom działać poprawnie jako "mosty" do sieci Ethernet. Definiuje jak mapować ramki i obsługiwać priorytety 802.1D.

### 802.11d - Global Harmonization
* [cite_start]**Co to:** "Regulatory Domains"[cite: 1754].
* **Cel:** AP rozgłasza kod kraju (np. PL, US) i dozwolone kanały/moce. Dzięki temu Twoja karta WiFi wie, że w Japonii nie może używać pewnych kanałów, a w USA innych.

### 802.11h - Spectrum Management (5 GHz)
* [cite_start]**Co to:** Zarządzanie widmem, wymagane w Europie dla 5 GHz[cite: 2145].
* **Mechanizmy:**
    * **TPC (Transmit Power Control):** Ograniczanie mocy nadawania, by nie zakłócać satelitów.
    * [cite_start]**DFS (Dynamic Frequency Selection):** Jeśli AP wykryje **radar** (np. pogodowy, wojskowy), musi natychmiast zmienić kanał[cite: 346, 348].

### 802.11k - Radio Resource Measurement
* [cite_start]**Co to:** Pomiary zasobów radiowych[cite: 381].
* **Działanie:** Klient może zapytać AP: "Jakie są inne AP w pobliżu?". AP wysyła **Neighbor Report**. Przyspiesza to roaming, bo klient nie musi skanować całego pasma "w ciemno".

### 802.11v - Wireless Network Management
* [cite_start]**Co to:** Zaawansowane zarządzanie siecią[cite: 436].
* **Funkcje:** Oszczędzanie baterii (dłuższy czas uśpienia), Load Balancing (AP może poprosić klienta: "przełącz się na inny AP, bo jestem przeciążony").