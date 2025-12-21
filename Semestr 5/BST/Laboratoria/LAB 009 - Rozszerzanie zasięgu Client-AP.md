**1. Metody zwiększania pokrycia sygnałem:**

- **Universal Repeater:** Urządzenie odbiera sygnał z głównego AP jako klient i jednocześnie retransmituje go jako nowy AP. Wada: Przepustowość spada o połowę, ponieważ radio musi naprzemiennie odbierać i nadawać te same dane.
    
- **WDS (Wireless Distribution System):** Most bezprzewodowy między AP, który pozwala zachować adresy MAC klientów (przezroczystość L2), ale wymaga wsparcia po obu stronach.
    

**2. Czynniki wpływające na wydajność w 802.11n:**

- **Technologia MIMO:** Wykorzystanie wielu anten (Tx/Rx) do przesyłania niezależnych strumieni danych (Spatial Multiplexing) lub poprawy jakości sygnału przez Beamforming.
    
- **Szerokość kanału:** Przełączenie z 20 MHz na 40 MHz teoretycznie podwaja prędkość, ale w zatłoczonym środowisku może zwiększyć liczbę zakłóceń.
    
- **Indeks MCS (Modulation and Coding Scheme):** Określa kombinację modulacji (np. 64-QAM) i kodu korekcyjnego. Wyższe MCS wymagają bardzo silnego sygnału i niskich szumów.
    

**Powiązania:**

- [[100 Standardy Podstawowe (a, b, g, n, ac, ax)]] – MIMO i MCS w standardzie 'n'.
    
- [[041 Struktura Ramki MAC]] – adresowanie w trybie WDS (4 adresy).