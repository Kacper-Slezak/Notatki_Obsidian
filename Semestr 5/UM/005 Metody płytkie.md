	PS. Gra w dwadzieścia pytań Kułakowski grał z córkami głównie w uniwersum           władcy pierścienia
# 1. Drzewa i Lasy
## 1. Drzewa decyzyjne

Chcemy tak zbudować drzewa aby w miarę możliwości dzieliło nam póle na dwie równe części
I doszło do poprawnej odpowiedzi.

- Jak zaprojektować drzewo?
	- szukamy pytań które podzielą zbiór (najlepiej w cechach 0/1 )
	- Metryka, która jest obiecująca jest Błąd średniokwadratowy:
		- sprawdzamy czy próbki w grupach są jednorodne po podziale na pod grupy
		- jeśli próbki są w miarę podobne **jest super**
		- wybieramy pytanie które jest najbardziej efektywne
	- Metryka z użyciem Entropii
	- Współczynnik Giniego (do liczenia różnicy dochodów w społeczeństwie)
- Sprawdza wszystkie opcje i wybiera najlepszy podział
- Nie pozwolić mu się przeuczyć 
- Dlaczego lubimy drzewa?
	- Łatwa interpretacja
	- Uniwersalność - nadają się do każdego typu danych
	- Normalizacja danych nie jest konieczna
	- Niski koszt obliczeniowy
- Dlaczego nie lubimy drzew?
	- Podatność na przeuczenie
		- aby unikać : 
			- przycinanie drzewa
			- minimalna liczba próbek w liściu 
			- maksymalna głębokość drzewa
	- Brak stabliności - po dodaniu nowych próbek drzewo musi się uczyć od nowa
	- Trudności z wychwyceniem zależności nie liniowych
	- Problemy z klasami dominującymi - potrzebne jest nadpróbkowanie mniej licznych klas
## 2. Las losowy

Używamy dużej ilości drzew, każde musi mieć inne parametry aby inaczej się wyuczyło 
Zbiór danych dla każdego drzewa powstaje przez losowanie (ze zwracaniem) próbek z głównego zbioru. Próbki się powtarzają między drzewami

- Jak połączyć decyzje wielu drzew?
	- Demokracja - głosowanie dla klasyfikacji
	- Dla regresji - średnia
- Podsumowanie:
	- Las jest dokładniejszy
	- Bardziej odporny na przeuczenie
	- Są w stanie sobie poradzić z brakującymi cechami
	- Trudniejsze w interpretacji, dlaczego podjęło taką decyzje
	- Bardziej złożone obliczeniowo
	- Szybki proces uczenia
	- Proste strojenie algorytmu
	- Dobrze się skalują, dobrze działają na dużych zbiorach danych
## 3. Wzmacnianie modelu

Idea: Tworzymy drzewo -> analizujemy dla jakich przypadków drzewo daje błędy -> dla każdej próbki zapisujemy błąd przewidywania -> te błędy są naszą nową etykietą -> tworzymy nowe drzewo, uczące się przewidywać błędy -> znowu szukamy błędów -> i tworzymy kolejne i kolejne i kolejne drzewo w oparciu o błędy poprzedniego -> iteracyjne poprawianie -> **Na koniec** składamy to wszystko w jedno super drzewo jest to suma decyzji tych drzew razy współczynnik shrinkage, aby nie przeuczyć 

- Zalety: 
	- większa skuteczność predykcji na małych przypadkach
	- Większa dokładność 
	- Chcemy wychwycić niuanse
	- Nie ma dużego sensu łączyć

# 2. K-NN 

Idea: Mamy zbiór danych i w zależności od x1 i x2, bierzemy próbkę z konkretnym x1 i x2, szukamy k najbliższych próbek, klasyfikacja - większościowa demokracja

- Cechy alg:
	- Prosty, łatwo interpretowalny
	- Próbka jest porównywana z innymi w zbiorze
	- Konieczna jest normalizacja cech
	- De facto nie ma uczenia tylko porównanie
	- Słabo się skaluje z liczbą cech (przekleństwo wielowymiarowości)
- Co znaczy bliski sąsiad ?
	- Miary podobieństwa i odległości
		- Najprostsza to odległość euklidesowa gdy mamy cechy numeryczne
		- Odległość Manhattan - suma wartości bezwzględniej cech, Różnica odległości w każdym wymiarze dodana do siebie
		 ![[Pasted image 20251024105744.png]]
		- Uogólnienie powyższych, odległość Minkowskiego ![[Pasted image 20251024105731.png]]
	- Podobieństwo consinusowe - jak bardzo podobne są do siebie dwa wektory (cosinus kąta między wektorami) ![[Pasted image 20251024105904.png]]
	- Dla cech kategorycznych ciężko mówić które są bliskie siebie, dlatego stosujemy odległość **Hamming'a** - liczba cech różnicujących próbki 
- Ile (k) warto mieć sąsiadów ?
	- Klasyfikacja koloru za pomocą różnych k ![[Pasted image 20251024110422.png]]
	- K - stroi algorytm który szuka w zależności od wartości albo lokalnie albo globalnie (trochę przypomina niedouczenie lub przeuczenie) 
	- Zazwyczaj stosujemy k o wartościach z przedziału od 3 do 15 (nieparzyste dla klasyfikacji)
	- Dostosujemy do potrzeb 
- Zastosowania:
	- Używamy do uzupełniania dziur w Dataset (scikit-learn: KNNInputer), próbuje przewidzieć możliwą wartość brakującej wartości cechy, szuka podobnych próbek i próbuje przewidywać. Jest to trochę ryzykowne, ale całkiem dobre
	- Świetnie się sprawdzają do lokalizacji bezprzewodowej (użyć w projekcie na koło), uśrednianie pozycji sąsiadów z wagami
	- Systemy rekomendacyjne 
	- Predykcja na niewielkich danych np. medycznych
# 3. Support Vector Machine

Idea: Lepiej się nadaje do klasyfikacji, Tworzymy hiperpłaszczyznę separującą dwie klasy z marginesem błędu, próbki leżące na marginesie nazywamy wektorami nośnych
- Równanie Hiperpłaszczyzny:
	- W przypadku dwuwymiarowym : ![[Pasted image 20251024111732.png]]
	- W przypadku trzywymiarowym : ![[Pasted image 20251024111802.png]]
	- Ogólny przypadek :![[Pasted image 20251024111815.png]]
- Funkcja kosztu to odwrotność marginesu hiperpłaszczyzny - algorytm porównuje różne hiper płaszczyzny 
	- Margines to :
	![[Pasted image 20251024112036.png]]
- Stosujemy soft i hard margin :
	- w przypadku dopuszczenia istnienia elementów po drugiej stronie tworzymy soft margin : 
	- Funkcja kosztu w soft margin ![[Pasted image 20251024112156.png]]

- Nieliniowy klasyfikator SVM: 
	- Dla danych które nie są łatwo podzielne 
	- Z danych dwuwymiarowych robimy trójwymiarowe 
		- Tworzymy cechę pochodną od dwóch poprzednich np. :![[Pasted image 20251024112524.png]]
		- W tym wypadku trzecia cecha to odległość od środka i teraz możemy ładnie wstawić hiperpłaszczyznę i ładnie dzieli dane
- Podsumowanie:
  - Działają jako klasyfikator
  - Dobrze sobie radzą na małych zbiorach
  - Są odporne na przeuczenie
  - Proces uczenia może być długi
  - Radzi sobie z próbkami odstającymi
  - Możliwe jest przekształcanie z użyciem funkcji nie linowych