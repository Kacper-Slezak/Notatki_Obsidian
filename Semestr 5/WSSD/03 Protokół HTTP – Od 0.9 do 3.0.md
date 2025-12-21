---
tags:
  - http
  - http2
  - http3
---


Ewolucja protokołu skupiała się na redukcji opóźnień (**Latency**).

### Ewolucja Wersji

1. **HTTP/1.1:** Wprowadził `Persistent Connections`, ale cierpi na **HOL Blocking** (Head-of-Line) – jeden wolny obiekt blokuje całą kolejkę w porcie TCP.
    
2. **HTTP/2:** * **Binary Protocol:** Zamiast tekstu, przesyła ramki binarne.
    
    - **Multiplexing:** Wiele zapytań w jednym połączeniu TCP.
        
    - **Header Compression (HPACK):** Oszczędność pasma.
        
    - **Server Push:** Serwer wysyła zasoby zanim klient o nie zapyta.
        
3. **HTTP/3 (QUIC):**
    
    - Przenosi warstwę transportu na **UDP**.
        
    - Rozwiązuje problem HOL na poziomie warstwy transportowej (utrata pakietu UDP nie blokuje innych strumieni).
        
    - **Connection Migration:** Umożliwia zmianę adresu IP (np. przełączenie z Wi-Fi na LTE) bez zrywania sesji.
        

> [!important] Struktura URL `https://user:password@host:port/path?query#fragment`
> 
> - Ciekawostka z wykładu: Host może być podany jako IP Decimal (np. `2130706433` dla localhost).

