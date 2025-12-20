---
alias:
  - Wykład 6 - Architektura i PHY
tags:
  - wyklad
  - architektura
  - phy
  - dsss
  - fhss
---
---

# Wykład 6: IEEE 802.11 Część I - Architektura i Warstwa Fizyczna

## 1. Wstęp i Motywacja
Standard 802.11 (WLAN) powstał, aby zapewnić mobilność i elastyczność tam, gdzie okablowanie jest trudne lub niemożliwe.

### Główne zalety WLAN
* **Mobilność:** Użytkownik ma dostęp do sieci w dowolnym miejscu zasięgu.
* **Elastyczność i Skalowalność:** Łatwe dodawanie nowych użytkowników i pokrycie trudnych obszarów (np. zabytki).
* **Niezawodność:** Odporność na uszkodzenia fizyczne (np. trzęsienia ziemi, pożar) - brak jednego centralnego kabla, który można przeciąć.
* **Koszt:** Niskie koszty instalacji (brak kucia ścian), choć koszt sprzętu bywa wyższy niż w Ethernet.

---

## 2. Architektura Sieci 802.11
Standard definiuje dwie najniższe warstwy modelu OSI: **PHY (fizyczną)** oraz **MAC (podwarstwę dostępu do medium)**.

### Elementy Składowe (Terminologia)
* **Station (STA):** Każde urządzenie z interfejsem 802.11 (laptop, smartfon, ale też Access Point).
* **Access Point (AP):** Stacja pełniąca funkcję mostu do systemu dystrybucyjnego (DS).
* **BSS (Basic Service Set):** Podstawowa komórka sieci. Grupa stacji pod kontrolą jednego AP (Infrastructure) lub połączonych bezpośrednio (Ad-hoc).
    * Obszar pokrycia nazywa się **BSA (Basic Service Area)**.
* **ESS (Extended Service Set):** Zbiór wielu BSS połączonych przez sieć szkieletową (DS). Użytkownik widzi to jako jedną dużą sieć (ten sam SSID).
* **DS (Distribution System):** System łączący punkty dostępowe (zazwyczaj Ethernet 802.3).
* **Portal:** Logiczny punkt styku, gdzie sieć 802.11 łączy się z inną siecią (np. przewodowym Internetem).

### Tryby Pracy
1.  **Infrastructure Mode:**
    * Wymaga AP.
    * Komunikacja zawsze przechodzi przez AP (nawet jeśli stacje są obok siebie).
    * AP buforuje ramki dla uśpionych stacji (oszczędzanie energii).
2.  **Ad-hoc Mode (IBSS - Independent BSS):**
    * Komunikacja bezpośrednia (Peer-to-Peer).
    * Brak AP, brak dostępu do sieci zewnętrznej (w standardowej konfiguracji).

---

## 3. Usługi (Services) w 802.11
Standard dzieli usługi na te dostarczane przez Stację (SS) i System Dystrybucyjny (DS).

| Typ Usługi | Nazwa | Opis |
| :--- | :--- | :--- |
| **Stacyjne (SS)** | Authentication | Uwierzytelnianie tożsamości stacji (przed asocjacją). |
| | Deauthentication | Zerwanie uwierzytelnienia. |
| | Privacy | Szyfrowanie danych (np. WEP/WPA). |
| | Data Delivery | Przesyłanie ramek MSDU (MAC Service Data Units). |
| **Dystrybucyjne (DS)** | Association | Rejestracja stacji w AP (tworzy mapowanie w DS). |
| | Disassociation | Wyrejestrowanie stacji z AP. |
| | Reassociation | Przełączenie się do innego AP (Roaming). |
| | Distribution | Przekazywanie ramek wewnątrz ESS (między AP). |
| | Integration | Przekazywanie ramek poza sieć 802.11 (przez Portal). |

> [!NOTE] Roaming
> Standard 802.11 definiuje usługę **Reassociation**, ale nie narzuca algorytmu *kiedy* stacja ma się przełączyć. Decyzja należy do sterownika karty sieciowej klienta.

---

## 4. Warstwa Fizyczna (PHY) - Legacy (1997)
Pierwsza wersja standardu oferowała 1 i 2 Mbps. Dzieliła się na podwarstwy:
* **PLCP (Physical Layer Convergence Procedure):** Dodaje preambułę i nagłówek fizyczny.
* **PMD (Physical Medium Dependent):** Odpowiada za modulację i wysyłanie bitów.

### A. Podczerwień (Infrared - IR)
* **Medium:** Światło podczerwone (850-950 nm), odbite (diffuse).
* **Modulacja:** **PPM (Pulse Position Modulation)**.
    * 4-PPM (2 bity/symbol) -> 1 Mbps.
    * 16-PPM (4 bity/symbol) -> 2 Mbps.
* **Wady:** Nie przenika przez ściany, zakłócane przez słońce. Obecnie nieużywane.

### B. FHSS (Frequency Hopping Spread Spectrum)
* **Zasada:** Sygnał "skacze" po częstotliwościach w pseudolosowej sekwencji.
* **Pasmo:** 2.4 GHz (ISM).
* **Kanały:** 79 kanałów (w USA/Europie) o szerokości **1 MHz**.
* **Parametry:**
    * **Modulacja:** **2-GFSK** (1 Mbps) lub **4-GFSK** (2 Mbps).
    * **Dwell Time:** Czas przebywania na kanale (max 390 ms).
    * **Hop Time:** Czas przeskoku (224 µs).
* **Zaleta:** Odporność na zakłócenia wąskopasmowe.

### C. DSSS (Direct Sequence Spread Spectrum)
Technologia, która stała się podstawą Wi-Fi (802.11b).
* **Zasada:** Każdy bit danych jest mnożony (XOR) przez ciąg rozpraszający.
* **Barker Code:** Ciąg 11-bitowy `+1, -1, +1, +1, -1, +1, +1, +1, -1, -1, -1`. Zapewnia zysk przetwarzania (Processing Gain) ok. 10.4 dB.
* **Modulacja:**
    * **DBPSK** (Differential Binary PSK) -> 1 Mbps.
    * **DQPSK** (Differential Quadrature PSK) -> 2 Mbps.
* **Kanały:** Szerokość **22 MHz**. W paśmie 2.4 GHz mieszczą się tylko **3 niepokrywające się kanały** (1, 6, 11).
    * Odstęp między środkami kanałów to 5 MHz.

> [!summary] Podsumowanie PHY
> DSSS wygrało z FHSS, ponieważ łatwiej było je skalować do wyższych prędkości (11 Mbps w 802.11b używa CCK zamiast Barkera, ale zachowuje kanał DSSS).