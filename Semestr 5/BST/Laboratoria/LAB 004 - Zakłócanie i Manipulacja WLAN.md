**1. Nadużycia ramek zarządzających i kontrolnych:**

- **Beacon Flooding:** Atakujący generuje tysiące fałszywych ramek Beacon z różnymi SSID. Powoduje to „zniknięcie” prawdziwej sieci na liście wyboru u klienta oraz może doprowadzić do zawieszenia sterownika karty sieciowej skanującej pasmo.
    
- **Deauthentication Attack:** Wysyłanie sfałszowanej ramki Deauthentication (podszywając się pod AP lub klienta). Ponieważ ramki te w starszych standardach nie są szyfrowane (brak 802.11w), każda stacja natychmiast przerywa połączenie.
    

**2. Ataki na mechanizm dostępu do medium (MAC Layer):**

- **RTS/CTS Flood:** Atakujący wysyła ramki RTS (Request to Send) z ustawionym bardzo dużym czasem trwania w polu _Duration_. Wszystkie stacje w zasięgu ustawiają swój wektor NAV (Network Allocation Vector) i milkną na długi czas, sądząc, że medium jest zarezerwowane.
    
- **Manipulacja oknem rywalizacji (CW Cheating):** Użytkownik może ręcznie ustawić parametry CWmin​ i CWmax​ na bardzo niskie wartości (np. 1). Taka stacja prawie zawsze wygrywa rywalizację o medium, drastycznie ograniczając przepustowość innym, uczciwym użytkownikom.
    

**Powiązania:**

- [[040 Warstwa MAC i Dostęp (DCF, PCF)]] – działanie NAV i Backoff.
    
- [[041 Struktura Ramki MAC]] – znaczenie pola Duration.