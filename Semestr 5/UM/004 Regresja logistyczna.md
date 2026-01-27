
# Po co ?

1. Służy do klasyfikacji - dopasowanie obiektów do danej klasy np. rozpoznawanie obiektów, chorób 
2. Hipoteza w regresji logistycznej różni się od liniowej obłożeniem jej exponentą
	- h(x) = g ( θ xT ) = 1/(1 + exp(-θxT))
## Problemy bias/variance

1. W uczeniu maszynowym najwięszkymi problemami jest zawsze przeucznie i niedouczenie 
2. Zarówno w regresji logistycznej jak i liniowej ten problem występuje
#### Jak go rozwiązać ? 

- Nie douczenie ?
	1. Zwiększyć wymiar danych np. dodać nowe cechy
	2. zwiększyć wymiar danych np. dodać wielomiany lub inne funkcje już istniejących danyc h
	3. Ogólnie problemem jest to że model jest zbyt prosty
- Przeuczenie ?
	1. Zmniejszyć wymiar danych np. usunąć wybrane cechy
	2. Zastosować regularization czyli. zmniejszeni współczynników 0teta
	3. Mamy za mało próbek danych 
### Regularyzacja dla regresji liniowej

1. do funkcji kosztu dodajmy współczynnik regularyzacji
2. Do algorytmu gradient descent dodajemy współczynnik przy teta troche mniejszy od zera 


## Diagnostyka:
1. Dodać więcej danych wejściowych (high variance)
2. Zwiększyć wymiar danych dodać liczbę cech (high bias)
3.  Większa siła regularyzacji (high variance)
4. 