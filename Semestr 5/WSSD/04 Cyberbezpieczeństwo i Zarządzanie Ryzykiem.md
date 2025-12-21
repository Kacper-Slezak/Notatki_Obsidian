---
tags:
  - bezpieczeństwo
  - CIA
---


Bezpieczeństwo to proces, a nie produkt.

### Triada CIA

1. **Confidentiality (Poufność):** Szyfrowanie, kontrola dostępu.
    
2. **Integrity (Integralność):** Sumy kontrolne, podpisy cyfrowe.
    
3. **Availability (Dostępność):** Anty-DDoS, redundancja.
    

### Zarządzanie Podatnościami

- **Risk = Probability x Impact**.
    
- **CVE (Common Vulnerabilities and Exposures):** Katalog konkretnych błędów.
    
- **CVSS (Common Vulnerability Scoring System):** Skala 0-10 określająca powagę błędu.
    
- **Secure by Design:**
    
    - **Zero Trust:** "Nigdy nie ufaj, zawsze weryfikuj". Każde żądanie musi być uwierzytelnione, nawet wewnątrz sieci lokalnej.
        
    - **Secrets Management:** Nigdy nie trzymaj haseł w kodzie (użyj Vault).