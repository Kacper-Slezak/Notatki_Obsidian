---
tags:
  - wykład
  - bezpieczeństwo
  - wpa2
  - 8021x
  - 80211h
  - radius
alias:
  - Wykład 11 - Bezpieczeństwo i 802.11h
---
# Wykład 11: IEEE 802.11 Część VI - Bezpieczeństwo i 5 GHz

## 1. IEEE 802.11h (Spectrum Managed 5 GHz)
Rozszerzenie wymuszone przez regulacje europejskie (ETSI) dla pasma 5 GHz, aby Wi-Fi nie zakłócało radarów i satelitów.
Wprowadza dwa obowiązkowe mechanizmy dla urządzeń 5 GHz (szczególnie outdoor):

1.  **DFS (Dynamic Frequency Selection):**
    * AP musi nasłuchiwać sygnałów radarowych przed użyciem kanału (CAC - Channel Availability Check).
    * W trakcie pracy (In-Service Monitoring), jeśli wykryje radar -> musi natychmiast opuścić kanał i powiadomić klientów (Channel Switch Announcement).
2.  **TPC (Transmit Power Control):**
    * Dynamiczna regulacja mocy.
    * Urządzenia muszą nadawać z najniższą możliwą mocą (o 3 dB niższą od max), aby utrzymać link margin. Zmniejsza to zakłócenia dla innych systemów.

---

## 2. IEEE 802.11i (Bezpieczeństwo - WPA2)
Zastępuje dziurawe WEP. Definiuje architekturę **RSN (Robust Security Network)**.

### Filary Bezpieczeństwa 802.11i
1.  **Uwierzytelnianie (Authentication):** IEEE 802.1X (Port-based Network Access Control).
2.  **Zarządzanie Kluczami (Key Management):** 4-Way Handshake.
3.  **Szyfrowanie (Data Privacy):** CCMP (AES) lub TKIP (RC4 - legacy).

### 802.1X i EAP (Extensible Authentication Protocol)
W sieciach Enterprise nie używa się wspólnego hasła. Każdy użytkownik ma swoje poświadczenia.
* **Supplicant:** Klient (np. laptop).
* **Authenticator:** Access Point (blokuje port, przepuszcza tylko ramki EAPOL).
* **Authentication Server:** Serwer RADIUS (weryfikuje usera).

**Typy EAP:**
* **EAP-TLS:** Wymaga certyfikatów po obu stronach (Klient i Serwer). Najbezpieczniejszy, ale trudny we wdrożeniu.
* **EAP-TTLS / PEAP:** Certyfikat tylko na serwerze. Tworzy szyfrowany tunel TLS, w którym przesyła się hasło. Popularny w korporacjach/uczelniach (np. Eduroam).

### Procedura 4-Way Handshake
Proces generowania kluczy szyfrujących (PTK) z głównego klucza (PMK).

| Krok | Kierunek | Zawartość | Opis |
| :--- | :--- | :--- | :--- |
| **1** | AP -> STA | **ANonce** | AP wysyła losową liczbę. STA generuje PTK. |
| **2** | STA -> AP | **SNonce + MIC** | STA wysyła swoją losową liczbę i podpis (MIC). AP weryfikuje i generuje PTK. |
| **3** | AP -> STA | **GTK + MIC** | AP wysyła zaszyfrowany klucz grupowy (GTK) do broadcastów. |
| **4** | STA -> AP | **ACK** | Potwierdzenie. Port zostaje odblokowany. |

**Hierarchia Kluczy:**
* **PMK (Pairwise Master Key):** Klucz główny (z RADIUSa lub PSK).
* **PTK (Pairwise Transient Key):** Klucz sesji (unikalny dla każdej asocjacji). Składa się z: KCK (Confirmation), KEK (Encryption), TK (Temporal Key - szyfruje dane).

### Protokoły Szyfrowania
* **TKIP (Temporal Key Integrity Protocol):** "Łatka" na WEP. Używa RC4, ale zmienia klucz co pakiet (Per-packet key mixing) i ma dłuższy IV (48 bit). Używa "Michael" do sprawdzania integralności (MIC).
* **CCMP (Counter Mode with CBC-MAC Protocol):** Standard docelowy WPA2. Używa **AES** (blokowy). Bardzo bezpieczny.