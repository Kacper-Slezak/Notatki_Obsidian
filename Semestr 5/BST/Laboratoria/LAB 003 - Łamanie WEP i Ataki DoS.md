---
tags:
  - wep
  - rc4
---


**1. Istota problemu – dlaczego WEP upadł?**

- **Podatność wektora inicjującego (IV):** WEP używa 24-bitowego pola IV przesyłanego tekstem jawnym. Przy ograniczonej przestrzeni (ok. 16 milionów kombinacji) i dużym natężeniu ruchu, te same wartości IV powtarzają się bardzo szybko (kolizje IV).
    
- **Słabość algorytmu RC4:** WEP opiera się na szyfrze strumieniowym RC4, w którym kluczem jest połączenie stałego klucza sekretnego i zmiennego IV. Atakujący, analizując odpowiednio dużą liczbę pakietów z tymi samymi IV, może statystycznie wyliczyć klucz sekretny.
    

**2. Zaawansowane metody ataku (Klucz do egzaminu):**

- **FMS (Fluhrer, Mantin, Shamir):** Pierwszy klasyczny atak statystyczny oparty na „słabych IV”.
    
- **Korek:** Rozszerzenie ataku FMS przez hakera o tym samym pseudonimie, optymalizujące proces odzyskiwania klucza.
    
- **PTW (Pyshkin, Tews, Weinmann):** Obecnie najbardziej efektywna metoda, pozwalająca na złamanie klucza 104-bitowego w mniej niż 60 sekund przy zebraniu odpowiedniej liczby ramek (zwykle wystarczy kilkadziesiąt tysięcy pakietów ARP).
    
- **Chopchop:** Atak pozwalający na odszyfrowanie pakietu bajt po bajcie bez znajomości klucza, wykorzystujący brak mechanizmu sprawdzania integralności danych z nagłówkiem ramki (WEP używa liniowego CRC, który można łatwo zmanipulować).
    

**3. Procedura praktyczna (Narzędzia):**

- **Airmon-ng:** Przełączenie karty w tryb monitor.
    
- **Aireplay-ng:** Iniekcja ramek w celu wymuszenia na AP generowania nowych IV:
    
    - **Fake Authentication:** Skojarzenie z AP, aby ten akceptował nasze pakiety iniekcyjne.
        
    - **ARP Replay:** Przechwycenie pakietu ARP i jego masowe retransmitowanie, co zmusza AP do wysyłania odpowiedzi z nowymi, cennymi dla atakującego IV.
        

**Powiązania:**

- [[060 Bezpieczeństwo WLAN (802.11i)]] – sekcja o WEP.
    
- [[Wykład_8_IEEE_802.11_Zarzadzanie]] – szczegóły algorytmu RC4.