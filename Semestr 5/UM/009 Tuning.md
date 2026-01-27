# Hiperparametry

1. Wpływające na proces uczenia się modelu
	- learning rate 
	- batch size 
	- epochs 
	- regularization rate 
	- dropout 
2.  Wpływające na algorytm 
	- funkcja kosztu
	- optymalizatory
	- Funkcje aktywacji 
3. Wpływające na architekturę sieci 
	- liczba warstw 
	- liczba neuronów
	- Dla sieci splotowych:
		- wymiar filtru
		- krok
		- padding
		- typ poolingu
		- rozmiar poolingu
## Sposoby doboru parametrów

- **Grid Search** - sprawdza wszystkie kombinacje dla konkretnych zakresów parametrów, brute force
- **Random Search** - losowo wybiera kombinacje parametrów dla zadanych zakresów
- **Hyperband** - duża liczba kombinacji sprawdzana przez kilka mało epok, najbardziej obiecujący pod zbiór jest trenowany dłużej i tak w kółko 
- **BayesianOptimization** - kilka kombinacji jest sprawdzanych a kolejne są wybierane w zależności od wyników poprzednich kombinacji, bliżej nich lub dalej w przestrzeni hiperparametrów 

# Algorytmy Genetyczne

1. Jest to podejście heurystyczne czyli nie gwarantuje znalezienia najbardziej optymalnego rozwiązania dobrze nadaje się do obliczeń równoległych
2. Algorytm:
	1. Losuje grupę rozwiązań wybiera najlepszą podgrupe resztę odrzuca
	2. Tworzy pochodne rozwiązania poprzez
		- krzyżowanie crossover
		- losowe zmiany czyli mutacje wybranych parametrów
	3. Weryfikujemy to co nam wyszło z rozwiązań zostawiamy najlepsze i resztę odrzucamy
	4. Kroki 2 i 3 powtarzamy tak długo jak osiągniemy wynik który chcemy lub skończy nam się moc obliczeniowa

# Transfer Learning 

1. Chodzi o to że bierzemy wcześniej wytrenowany model na jakimś ogólnym zbiorze nad zbiorze naszych danych i do trenowujemy go na naszych danych 
2. Mrozimy sobie warstwy początkowe i środkowe ale podmieniamy i dotrenowujemy te ostatnie warstwy 

# Federated Learning 

1. Chodzi o rozsyłanie kopii modelu do urządzeń lokalnych
2. Trening na danych prywatnych 
3. Przesyłanie modeli lokalnych z powrotem do centrum obliczeniowego 
4. Aktualizacje głównego modelu na podstawie modeli lokalnych
### Zastosowania:

1. Sektor medyczny i bankowy
2. Urządzenia typu smartfony i IOT

### Co zyskujemy ? 

1. Prywatność i ochrona danych 
2. Wykorzystanie rozproszonych zasobów do obliczeń
### A co tracimy ?

1. Spójność danych w urządzeniach lokalnych 
2. Obciążenie urządzeń lokalnych 
3. Koszty komunikacji: przepustowość, opóźnienia