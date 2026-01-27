# Klasteryzacja
## Gdzie się przydaje?

1. Segmentacja rynku
2. Analiza sieci społecznościowych
3. Grupowanie wyników wyszukiwania
4. Wstępna analiza dużych zbiorów danych

## Algorytm centroidów

1. Losowo wybieramy środki klastrów
2. Iteracyjnie powtarzamy dwa kroki :
	1. przyporządkujemy punkty do klastrów
	2. aktualizujemy pozycje środków klastrów
	3. Funkcja kosztu J = 1/m Suma || x(i) - u(i) ||^2 - u to jest centroid klastra do którego należy i=ty punkt
3. Gdy żaden z punktów  nie zmienia swojej pozycji to algorytm osiągnął zbierzność

## Podsumowanie

1. Zastosowania: segmentacja rynku, analiza użytkowników w sieci, grupowanie dużych zbiorów danych
2. Algorytm: iteracje dwóch operacji - przydziału danych do klastrów i wyznaczanie centroidów klastrów
3. Sprawy, na które należy zwrócić uwagę:
	- Wybór i normalizacja danych wejściowych
	- inicjalizacja - losowa, środki klastrów w k spośród m punktów z danymi
	- możliwe lokalne minimum funkcji kosztu - warto wielokrotnie puścić algorytm
	- dobór liczby klastrów: wg zastosowania można spróbować łokcia

# Redukcja wymiarowości

## Zastosowania

1. Redukcja danych - przyśpieszenie ML
2. Wizualizacja np. do 2D/3D 

## Algorytm PCA
#### Cel
- dla danych n-wymiarowych zmniejszyć tą liczbę do k wymiarów
#### Algorytm 
- znaleźć k wektorów, wzdłuż których te dane są rozpięte 

### Matematyka PCA

1. Normalizujemy dane 
2. Liczymy macierz kowariancji:  COV = 1/m-1 * (Xt*X)
3. Wyznaczamy wektory i włąsnosci własne macierzy Cov = ULU^-1
4. Redukujemy wymiar danych Xpca(m x k) = X(m x k) Uk (n x k)
#### Jak wybrać liczbę wymiarów k ?

1. Wybieramy liczbę k pod nasze zastosowanie np. wizualizacja 2/3
2. Wybieramy jaki poziom informacji chcemy zachować (% of variance retained)\
![[Pasted image 20260123125016.png]]
wzór na procent zachowanych informacji

### Podsumowanie

1. Zastosowania: 
	1. usuniecie danych niosących jak najmniej informacji w celu przyspiesznia modelu
	2. wizualizacja
2. Algorytm PCA
	- normalizujemy dane
	- szukamy k wektorów ortogonalnych najlepiej rozpinających dane
	- robimy projekcje danych na te wektory 
3. Inne aspekty:
	- zastosowanie PCA to kompromis, bo redukcja wymiarów niesie za sobą koszt utraty informacji
	- PCA działa bez etykiet danych, nie jest metodą na overfiting

# Wykrywanie anomalii

### Gdzie się przyda ?

1. zastosowanie typu fraud detection
2. ataki sieciowe
3. monitoring produkcji, funkcjonowanie sprzętu
4. media społecznościowe

### Na czym polega ?

1. Wybieramy n cech które mogą wskazać potencjalna anomalię 
2. Dla każdej cechy z osobma liczymy parametr rozkłądu u i oq^2
3. Tworzymy iloczyn funkcji gęstości prawdopodobieństwa:
![[Pasted image 20260123141407.png]]
4. Przyjmujemy niewielką wartość progową e
	1. Można ją ustawić z góry
	2. Lub w przypadku zbioru danych z etykietami
		- na zbiorze treningowym gdzie mamy tylko typowe dane wyznaczamy parametry rozkłądu i p(x)
		- na zbiorze walidacyjnym gdzie mamy typowe plus anomalie dobieramy najlepsze e pod kątem np. F1-score
		- na zbiorze testowym wyznaczamy skutecznośćdla naszego e 
5. Dla każdego nowego przypadku próbki sprawdzamy czy p(x) < e jeśli tak to anomalia

### Kiedy co stosować ?

1. Model podstawowy 
	- wydajniejszy obliczeniowo lepszy przy dużej liczbie cech
	- można stosować przy n>m - mały zbiór duża liczba cech
2. Wielowymiarowy Gauss
	- bierze pod uwagę korelacje miedzy poszczególnymi zmiennymi
	- konieczne jest m>n
3. Detekcja anomalii
	- dane bezetykiet
	- dane z etykietami  - mało przypadków anomalii
4. Uczenie nadzorowane
	- dane z etykietami - dużo przypadków dla obu klas
	- przypadki pozytywne podobnego typu  łatwość uczenia

### Podsumowanie
1. Zastosowania:
	1. ataki sieciowe
	2. monitoring produkcji i działania sprzętu
	3. nietypowe zachowanie klientów/użytkowników
2. Warto starannie wybrać cechy wśród których szukamy anomalii
3. Dwie wersje algorytmu oparte na rozkładzie normalnym zwykłym, wielomianowym
4. Kluczowy jest parametr e
	- albo go określamy z góry
	- albo korzystamy z danych z etykietami aby go wyznaczyć
