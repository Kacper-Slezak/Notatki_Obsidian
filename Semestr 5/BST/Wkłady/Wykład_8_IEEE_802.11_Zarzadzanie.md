---
tags: [wykład, zarządzanie, power-save, wep, bezpieczeństwo, stany]
alias: [Wykład 8 - Zarządzanie i Bezpieczeństwo]
---
# Wykład 8: IEEE 802.11 Część III - Zarządzanie i Bezpieczeństwo

## 1. Zarządzanie (Management Functions)
Warstwa MAC to nie tylko dostęp do medium, ale też utrzymanie spójności sieci.

### Synchronizacja (TSF - Timing Synchronization Function)
Wszystkie stacje w BSS muszą mieć ten sam czas (np. do Frequency Hoppingu lub Power Save).
* **Infrastructure:** AP jest "mistrzem czasu". Wysyła **Beacony** z własnym znacznikiem czasu (Timestamp). Stacje aktualizują swoje zegary, aby dorównać do AP.
* **Ad-hoc (IBSS):** Algorytm rozproszony.
    * Każda stacja przygotowuje Beacon.
    * Po odczekaniu losowego czasu (backoff), pierwsza stacja wysyła Beacon.
    * Inne stacje, słysząc to, anulują swoje Beacony i przyjmują czas z odebranego (jeśli jest późniejszy).

### Zarządzanie Energią (Power Management)
Wi-Fi zużywa dużo energii. Stacje bateryjne (telefony) większość czasu spędzają w stanie uśpienia (**Doze**).
1.  **TIM (Traffic Indication Map):** Mapa bitowa przesyłana w każdym Beaconie. AP informuje uśpione stacje (po ich ID - AID), że ma dla nich zbuforowane dane.
2.  **DTIM (Delivery TIM):** Licznik (np. co 3 Beacony), który wyznacza moment wysłania danych grupowych (**Broadcast/Multicast**). W tym momencie *wszystkie* stacje muszą się obudzić.
3.  **PS-Poll (Power Save Poll):** Ramka sterująca wysyłana przez stację po wybudzeniu (jeśli zobaczyła swój bit w TIM). Służy do "wyciągnięcia" pojedynczej ramki danych z bufora AP.

---

## 2. Maszyna Stanów (State Machine)
Zanim stacja wyśle dane, musi przejść przez proces przyłączania.

| Stan | Nazwa | Dozwolone Ramki | Opis |
| :--- | :--- | :--- | :--- |
| **1** | **Unauthenticated, Unassociated** | Class 1 (Beacon, Probe, Auth) | Stan początkowy. Stacja "widzi" sieć, ale sieć jej nie zna. |
| **2** | **Authenticated, Unassociated** | Class 1 + 2 (Assoc, Reassoc) | Stacja potwierdziła tożsamość (Authentication), ale nie jest jeszcze członkiem BSS. |
| **3** | **Authenticated, Associated** | Class 1, 2, 3 (Data, PS-Poll) | Pełne połączenie. AP przekazuje ruch stacji do systemu dystrybucyjnego (DS). |

> [!warning] Roaming (Reassociation)
> Przełączenie się między AP (Roaming) to technicznie **Reassociation**. Pozwala to przenieść kontekst stacji (np. zbuforowane ramki) ze starego AP do nowego, o ile są połączone protokołem IAPP (lub 802.11r).

---

## 3. Bezpieczeństwo - Legacy (WEP)
**WEP (Wired Equivalent Privacy)** miał dać prywatność "równoważną kablowi". Okazał się kompletną porażką.

### Mechanizm działania
1.  **Szyfr:** RC4 (strumieniowy).
2.  **Klucz:** Sekret (40 lub 104 bity) + **IV (Initialization Vector - 24 bity)**.
3.  **XOR:** $Ciphertext = Plaintext \oplus RC4(Key || IV)$.
4.  IV jest przesyłany jawnym tekstem w każdej ramce.

### Dlaczego WEP jest słaby? (Kluczowe na egzamin)
* **Krótki IV (24 bity):** Pula $2^{24}$ (ok. 16 mln) wyczerpuje się w kilka godzin w ruchliwej sieci. Powtórzenie IV (IV Collision) przy tym samym kluczu pozwala łatwo odszyfrować dane (atak statystyczny).
* **Słabe IV (Weak IVs):** Niektóre wektory IV generują przewidywalny początek strumienia klucza RC4 (atak FMS/KoreK pozwalał złamać klucz w minuty).
* **Brak zarządzania kluczami:** Wszyscy użytkownicy mają ten sam klucz (PSK).
* **Liniowe CRC (ICV):** Możliwość modyfikacji zaszyfrowanej wiadomości bez znajomości klucza (Bit-flipping attack).

---

## 4. Ataki na sieci WLAN
* **Pasywne:** Nasłuch (Eavesdropping), Analiza ruchu.
* **Aktywne:**
    * **Rogue AP:** Podstawienie fałszywego AP ("Honeypot") z takim samym SSID.
    * **DoS (Denial of Service):**
        * **Jamming:** Fizyczne zagłuszanie pasma.
        * **Deauth Flood:** Wysyłanie fałszywych ramek *Deauthentication* (podszywając się pod AP), co rozłącza klientów.
        * **Virtual Jamming (NAV Attack):** Wysyłanie ramek (np. RTS) z ogromną wartością w polu *Duration*, zmuszając inne stacje do milczenia.