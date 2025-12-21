**1. Analiza typów ramek w Wireshark:**

- **Beacon:** Ramka zarządzająca wysyłana cyklicznie przez AP (zwykle co 100 TU). Zawiera SSID, parametry PHY, obsługiwane prędkości oraz mapę TIM (Traffic Indication Map) dla stacji w trybie oszczędzania energii.
    
- **RTS/CTS (Request to Send / Clear to Send):** Mechanizm ochrony przed problemem "ukrytej stacji". CTS rezerwuje medium (ustawia NAV) u wszystkich stacji słyszących odbiorcę, nawet jeśli nie słyszą one nadawcy.
    
- **NULL Data:** Pusta ramka danych używana przez klienta do informowania AP o przejściu w tryb uśpienia (Power Management bit).
    

**2. Procesy MAC:**

- **Skanowanie (Scanning):** Aktywne (wysyłanie Probe Request) pozwala na szybsze wykrycie sieci, podczas gdy pasywne (nasłuch Beacon) oszczędza baterię stacji.
    
- **Adresowanie:** Ramka może zawierać do 4 adresów MAC. W standardowej komunikacji infrastrukturalnej (STA <-> AP) Adres 1 to odbiorca radiowy, Adres 2 to nadawca radiowy, a Adres 3 służy do identyfikacji źródła/celu w sieci DS (np. MAC routera).
    

**Powiązania:**

- [[041 Struktura Ramki MAC]] - Format nagłówka.
    
- [[042 Zarządzanie i Stany]] - Skanowanie i Power Save.