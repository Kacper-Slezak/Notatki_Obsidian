\	jak podawać słowa jako dane wejściowe?
### Przetwarzanie języka naturalnego:

1. Wstępne przetwarzanie danych:
	- czyszczenie tekstów
	- podział na elementy podstawowe - tokeny
	- normalizacja
2. Transformacje 
	- fakt wystąpienia
	- zliczania ile razy występuje
	- zanurzenie
3. Możemy potem uczyć model

# Zanurzenia

1. Wielowymiarowa i ciągła oraz podlegającą uczeniu reprezentacja wartości kategorycznych powiązanych semantycznie 
2. Słowa występujące w zbliżonym kontkście ( do interpretacji własnej ) zajmują zbliżone położenie w takiej przestrzeni
3. Nie jest to interpretowalne nie wiemy co oznacz konkretna wartość w wektorze zanurzenia
4. Używamy uczenia nie nadzorowanego aby model sam sobie tworzył statystyki
5. Zbieżność wartości na konkretnych pozycjach wskazuje na wykrycie istotnego podobieństwa
6. Najbardziej użyteczny wskaźnik podobnieństwa to podobieństwo cosinusowe
	1. Cosinus kąta miedzy wektorami je reprezentującymi powinien być bliski