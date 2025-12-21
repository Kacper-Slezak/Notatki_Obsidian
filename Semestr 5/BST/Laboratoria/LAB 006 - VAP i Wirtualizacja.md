---
tags:
  - wirtualizacja
  - vap
  - iptables
---


**1. Koncepcja wirtualizacji interfejsów:**

- **VIF (Virtual Interface):** Możliwość zdefiniowania wielu logicznych sieci (np. „Office” i „Guest”) na jednym fizycznym radiu.
    
- **Izolacja i bezpieczeństwo:** Sieć gościnna powinna posiadać oddzielną adresację IP i być odizolowana od sieci głównej.
    

**2. Mechanizmy zarządzania ruchem:**

- **AP Isolation:** Funkcja uniemożliwiająca bezpośrednią komunikację między klientami podłączonymi do tego samego VAP. Klient może komunikować się tylko z bramą domyślną (internetem).
    
- **Bandwidth Limitation (tc):** Wykorzystanie narzędzia `tc` (Traffic Control) w systemie Linux do ograniczania przepustowości dla konkretnego interfejsu wirtualnego (np. limit 1 Mbps dla gości).
    
- **Firewall (iptables):** Reguły blokujące dostęp z sieci „Guest” do panelu administracyjnego routera oraz do zasobów sieci „Office”.