---
tags:
  - dns
---

DNS to hierarchiczna i rozproszona baza danych.

### Proces Rozwiązywania (Resolving)

1. **Recursive Query:** Klient pyta `Resolver` (np. 8.8.8.8) – "Znajdź mi adres". Resolver bierze na siebie całą pracę.
    
2. **Iterative Query:** Resolver odpytuje po kolei:
    
    - **Root Servers** (`.`) -> Zwraca serwery TLD.
        
    - **TLD Servers** (`.pl`) -> Zwraca serwery autorytatywne.
        
    - **Authoritative Servers** (`agh.edu.pl`) -> Zwraca konkretny adres IP.
        

### Rekordy DNS (Tabela Egzaminacyjna)

|Typ|Opis|
|---|---|
|**A**|Mapowanie nazwy na IPv4|
|**AAAA**|Mapowanie nazwy na IPv6|
|**CNAME**|Alias (nazwa wskazuje na inną nazwę)|
|**MX**|Mail Exchange (serwer poczty, ma priorytet)|
|**NS**|Name Server (serwer odpowiedzialny za strefę)|
|**SOA**|Start of Authority (parametry strefy, nr seryjny)|
> [!danger] Ataki na DNS
> 
> - **DNS Poisoning:** Wstrzyknięcie fałszywych danych do cache serwera.
>     
> - **DNSSEC:** Rozwiązanie. Podpisuje rekordy cyfrowo, zapewniając ich autentyczność.
>     
