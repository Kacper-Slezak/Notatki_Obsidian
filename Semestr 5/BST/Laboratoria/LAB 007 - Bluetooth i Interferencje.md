---
tags:
  - bluetooth
---


**1. Architektura Bluetooth:**

- **Piconet:** Sieć utworzona przez jedną stację Master i do siedmiu stacji Slave.
    
- **Profile Bluetooth:** Definiują rodzaj przesyłanych danych. Kluczowe to:
    
    - **PAN (Personal Area Network):** Tworzenie sieci IP przez Bluetooth.
        
    - **Serial Port Profile:** Bezprzewodowy zamiennik kabla szeregowego.
        
    - **HID (Human Interface Device):** Klawiatury i myszki.
        

**2. Problem interferencji w paśmie 2.4 GHz:**

- **Konflikt technologiczny:** Zarówno Bluetooth, jak i 802.11b/g/n pracują w tym samym paśmie.
    
- **Mechanizm zakłóceń:** Bluetooth używa FHSS (częste skoki po kanałach 1 MHz), podczas gdy WLAN używa szerokich kanałów (20-22 MHz). Gdy skok Bluetooth trafi w częstotliwość aktualnie używaną przez WLAN, dochodzi do kolizji pakietów.
    
- **Skutek:** Wzrost liczby błędów (BER), spadek przepustowości (Throughput) i wydłużenie opóźnień w obu sieciach.
    

**Powiązania:**

- [[030 Warstwa Fizyczna Legacy (FHSS, DSSS, IR)]] – zasada działania FHSS.
    
- [[010 Wstęp i Pasma Radiowe]] – zatłoczenie pasma 2.4 GHz.