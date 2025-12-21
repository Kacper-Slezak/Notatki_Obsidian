**1. Mechanizm WPA-PSK (Personal):**

- **4-Way Handshake:** Proces wymiany Nonce (liczb losowych) między AP a STA w celu wygenerowania klucza sesji (PTK) bez przesyłania hasła przez sieć. Podatność polega na tym, że jeśli przechwycimy tę wymianę, możemy przeprowadzić atak słownikowy/brute-force offline.
    

**2. Optymalizacja ataków (Rainbow Tables):**

- **Problem:** Obliczanie skrótu PMK (Pairwise Master Key) jest najbardziej obciążającym procesem (4096× HMAC-SHA1). Ponieważ PMK zależy od SSID, tradycyjne słowniki są wolne.
    
- **Pyrit:** Narzędzie pozwalające na użycie wstępnie przeliczonych baz skrótów (Rainbow Tables). Przyspiesza to łamanie klucza tysiące razy, pod warunkiem, że SSID sieci znajduje się w bazie.
    

**3. Podatność WPS (Wi-Fi Protected Setup):**

- **PIN Method:** 8-cyfrowy PIN jest sprawdzany przez AP w dwóch częściach (4 cyfry + 3 cyfry i suma kontrolna). Redukuje to przestrzeń poszukiwań z 100 mln do zaledwie 11 tysięcy kombinacji, co narzędzie **Reaver** potrafi złamać w kilka godzin.
    

**Powiązania:**

- [[060 Bezpieczeństwo WLAN (802.11i)]] - Teoria WPA2.