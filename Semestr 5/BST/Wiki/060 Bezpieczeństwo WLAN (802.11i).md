---
tags:
  - security
  - wep
  - wpa2
  - 8021x
  - szyfrowanie
---
# Bezpieczeństwo Sieci WLAN (IEEE 802.11i)

Ewolucja od "dziurawego" WEP do bezpiecznego WPA2/3.

## 1. WEP (Wired Equivalent Privacy) - Przestarzały
* **Szyfrowanie:** **RC4** (strumieniowe).
* **Klucz:** 40-bit lub 104-bit + **24-bitowy IV (Initialization Vector)**.
* **Problemy:**
    * **Krótki IV:** Powtarza się co kilka godzin (kolizje IV). To pozwala odzyskać klucz.
    * **Liniowe CRC (ICV):** Podatność na zmianę bitów w locie (Bit-flipping attack).
    * Brak zarządzania kluczami (ten sam klucz na wszystkich laptopach).

## 2. WPA (Wi-Fi Protected Access) - Przejściowy
Wprowadzony jako "łatka" programowa na karty WEP. Implementuje część standardu 802.11i.
* **Protokół:** **TKIP** (Temporal Key Integrity Protocol).
* **Mechanizmy naprawcze (na silniku RC4):**
    * **48-bitowy IV:** Zapobiega powtórzeniom (chroni przed Replay Attack).
    * **Per-packet Key Mixing:** Każdy pakiet ma inny klucz szyfrujący.
    * **MIC (Message Integrity Code):** Algorytm "Michael" chroniący integralność (zamiast słabego CRC).

## 3. WPA2 (IEEE 802.11i) - Standard Docelowy
Wymaga nowego sprzętu (akceleratorów AES).
* **Protokół:** **CCMP** (Counter Mode with CBC-MAC Protocol).
* **Szyfrowanie:** **AES** (Advanced Encryption Standard) w trybie licznikowym (Counter Mode).
* **Integralność:** CBC-MAC. Uważane za bardzo bezpieczne.

## 4. Architektura RSN (Robust Security Network) i 802.1X
Dla firm (Enterprise) używa się **802.1X**. Składniki:
1.  **Supplicant:** Klient (np. laptop).
2.  **Authenticator:** Access Point (blokuje port do czasu zalogowania).
3.  **Authentication Server:** Serwer **RADIUS** (trzyma bazę użytkowników).

**Protokoły EAP (Extensible Authentication Protocol):**
* **EAP-TLS:** Wymaga certyfikatów po obu stronach (najbezpieczniejszy, trudny w wdrożeniu).
* **EAP-TTLS / PEAP:** Certyfikat tylko na serwerze. Tworzy szyfrowany tunel, wewnątrz którego przesyła się hasło (np. MS-CHAPv2).

## 5. Procedura 4-Way Handshake
Kluczowy proces wymiany kluczy (generowanie PTK z PMK).
> [!procedure] Krok po kroku
> 1.  **AP -> STA:** Wysyła **ANonce** (Losowa liczba AP).
> 2.  **STA -> AP:** Wysyła **SNonce** (Losowa liczba STA) + **MIC**.
>     * *Teraz obie strony mogą obliczyć klucz sesji PTK.*
> 3.  **AP -> STA:** Wysyła **GTK** (Group Key - do broadcastów) zaszyfrowany kluczem PTK + **MIC**.
> 4.  **STA -> AP:** Potwierdzenie (**ACK**). Port zostaje otwarty.

**Klucze:**
* **PMK (Pairwise Master Key):** Klucz główny (z hasła PSK lub z serwera RADIUS).
* **PTK (Pairwise Transient Key):** Klucz sesji (szyfruje dane unicast).
* **GTK (Group Temporal Key):** Klucz grupowy (szyfruje broadcast/multicast).