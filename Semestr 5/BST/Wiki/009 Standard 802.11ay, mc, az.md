# Standard 802.11ay 

- Kolejna generacja sieci 60 GHz
- Rozwinięcie standardu [[007 Standard 802.11aa, ac, ad, ae, af, ah, ai, aj, ak, aq|ad]] 

1. Standard celuje w przepustowość 20 Gbit/s a teoretyczny maks to 250 Gb/s 
2. Funkcja Channel Bonding i Agregacja = pozwala na łączenie i agregacje sąsiednich kanałów co zwiększa dostępne pasmo transmisji
3. Wsparcie dla MIMO wspiera SU-MIMO oraz MU-MIMO(downlink) do 8 strumieni przestrzennych
4. Multiplexing polaryzacyjny - używa polaryzacji anten do wysyłania niezależnych strumieni danych używając polaryzacji
#### Zastosowania:

- bezprzewodowe wideo 8k
- systemy AR/VR
- stacje dokujace
- połączenia między szafami serwerowymi

# Standard 802.11mc

- Standard skupiający się na lokalizowaniu urządzeń i mierzeniu odległości
- wprowadził mechanizm Fine Timing Measurements (FTM)
	- zamiast polegać na mało precyzyjnej sile sygnału FRM mierzy czas przeloty sygnału w obie strony RTT 
	- na podstawie czasu obliczana jest odległość z dokładnością co do metra

# Standard 802.11az

- Ulepszony 802.11mc 
- Wyższa dokładność:
	- dzięki MIMO oraz szerszym kanałą oferuje lepszą precyzje nawet w warunkach bez bezpośredniej widoczności
- Oprócz czasu mierzy również kąt nadejścia i kąt odejścia sygnału i jego faze co pozwala na triangulację
- Bezpieczeństwo
	- Wprowadza mechanizmy chroniące przed fałszowaniem lokalizacji
	- poprzez zabezpieczenie sekwencji pomiarowych w warstwie fizycznej
- Pasywna lokalizacja - lokalizowanie wielu użytkowników jednocześnie bez generowania dodatkowego obciążenia sieci dla każdego z nich z osobna z