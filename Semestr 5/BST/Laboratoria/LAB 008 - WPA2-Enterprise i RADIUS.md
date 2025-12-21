---
tags:
  - wpa2
  - 8021x
  - eap
  - zarządzanie
---


**1. Architektura 802.1X (RSN):**

- **Supplicant:** Klient (laptop/smartfon).
    
- **Authenticator:** AP lub Switch. Blokuje ruch do czasu pomyślnego uwierzytelnienia. Przekazuje ramki EAP między klientem a serwerem.
    
- **Authentication Server (AS):** Serwer RADIUS (np. FreeRadius), który weryfikuje tożsamość w bazie danych.
    

**2. Szczegółowa analiza typów EAP (Extensible Authentication Protocol):**

- **EAP-MD5:** Przesyła tylko skrót MD5 hasła. Brak wzajemnego uwierzytelnienia (klient nie wie, czy łączy się z prawdziwym serwerem). Bardzo podatny na ataki słownikowe offline.
    
- **EAP-TLS:** Najbezpieczniejszy. Wymaga certyfikatów X.509 zarówno na serwerze, jak i u każdego klienta. Trudny w zarządzaniu (wymaga PKI).
    
- **PEAP (Protected EAP) / EAP-TTLS:** Kompromis. Tylko serwer musi mieć certyfikat. Tworzony jest bezpieczny tunel TLS, wewnątrz którego przesyłane jest hasło użytkownika (np. przez bezpieczniejszy protokół MS-CHAPv2). Jest to najczęstsze wdrożenie w firmach.
    

**3. Proces komunikacji:**

- Ramki **EAPOL (EAP over LAN)** są używane na łączu radiowym. AP "przepakowuje" je w pakiety **RADIUS** (UDP, porty 1812/1813) i przesyła do serwera.
    

**Powiązania:**
- [[060 Bezpieczeństwo WLAN (802.11i)]] - Standard 802.11i.