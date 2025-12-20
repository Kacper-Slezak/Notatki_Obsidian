---
tags: [standardy, phy, high-throughput]
---
# Standardy Podstawowe (Wydajnościowe)

[cite_start]Tutaj znajdują się główne standardy określające prędkość i pasmo[cite: 1727, 2061].

| Standard | Rok | Pasmo | Modulacja | Max Prędkość | Kluczowa Cechy |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **802.11** | 1997 | 2.4 GHz | DSSS/FHSS | 2 Mbps | "Legacy", IR (podczerwień) - rzadkość. |
| **802.11b** | 1999 | 2.4 GHz | HR-DSSS (CCK) | 11 Mbps | [cite_start]Duży zasięg, niska prędkość[cite: 1688]. |
| **802.11a** | 1999 | 5 GHz | OFDM | 54 Mbps | [cite_start]Mały zasięg, duża prędkość, więcej kanałów[cite: 1610]. |
| **802.11g** | 2003 | 2.4 GHz | ERP-OFDM | 54 Mbps | [cite_start]Kompatybilność z 'b', prędkość jak w 'a'[cite: 2056]. |
| **802.11n** | 2009 | 2.4/5 GHz | HT-OFDM | 600 Mbps | [cite_start]**MIMO**, Kanał 40MHz, Agregacja ramek[cite: 389]. |
| **802.11ac** | 2013 | 5 GHz | VHT-OFDM | ~6.9 Gbps | [cite_start]**MU-MIMO**, Kanał do 160MHz, 256-QAM[cite: 488]. |
| **802.11ax** | 2019 | 2.4/5 GHz | HE-OFDMA | ~9.6 Gbps | [cite_start]**Wi-Fi 6**, OFDMA, 1024-QAM, BSS Coloring[cite: 527]. |

> [!abstract] Anomalia Wydajności (Performance Anomaly)
> W sieciach mieszanych (np. 11b + 11g), wolniejsze stacje (11b) zajmują medium przez dłuższy czas, co drastycznie obniża wydajność szybkich stacji (11g) do poziomu tych wolnych. [cite_start]Mechanizm "uczciwości" (fairness) 802.11 jest tu wadą[cite: 1731].