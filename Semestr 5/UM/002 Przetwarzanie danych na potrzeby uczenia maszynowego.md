## Etapy obróbki danych
1. Przygotowanie danych
2. Identyfikacja typu danych (cech, zmiennych, atrybtutów)
3. Analiza statystyczna zmiennych indywidualnych
4. Analiza statystyczna relacji między zmiennymi
5. Postępowanie z elementami odstającymi
6. Inżynieria cech (wybór, ekstrakcja, transformacje)
7. Postępowanie z duplikatami
8. Postępowanie z brakami
9. Rozszerzenie danych
## Przygotowanie danych
### Etapy:

1. Przeglądnąć je najpierw
2. Pobrać, przeformatować
3. Etykietować
### Typy Danych

1. Kategoryczne - można je etykietować liczbami naturalnymi
	- nominalne - bez uporządkowanie
	- porządkowe - dające się uporządkować np. wykształcenie
2. Numeryczne -  z natury mierzalne
	- przedziałowe - można na nich wykonywać obliczenia, ale wartość zerowa jest umowna
	- ilorazowe/stosunkowe  - możemy wykonywać na nich obliczenia ale wartośźć zerowa ma mocne znaczenie
3. Istnieją typy danych do których nie odnosi się powyższa klasyfikacja przygotowanie tych danych wykonujemy z użyciem narzędzi uczenia maszynowego np używamy zanurzeń 
	- język naturalny
	- adres IP
	- dane typu grafowego
### Kodowanie cech

1. W przypadku danych kategorycznych należy je zakodować czyli przedstawić jako wektor liczbowy:
	- przypisujemy danym wartości dyskretne 
	- nie powinniśmy zakładać, że podajemy informacje o np. odległości 
	- przykład: szeregowiec → 1, kapral → 5, major → 20, generał → 100.
	- jeśli dane są tylko dychotomiczne zmian wartości na zero-jedynkowe to najłatwiejsze kodowanie binarne
	- Jednak jak możliwości jest więcej niż dwie to możemy używać różnych podejść
	- Możliwość przypisania kolejnych wartości: A → 1, B → 2, C → 3 (j. ang. label encoding). Wady!
	- Zespół zmiennych sztucznych, w sposób złożony kodujący opcje, np. A → 00, B → 01, C → 10, D → 11 (też nazywane kodowaniem binarnym; j. ang. binary encoding). Wady: czy D = B + C?
	- Najbardziej popularna opcja: one hot encoding: 
		- Przykład (wyróżnione 5 kolorów): czerwony → 10000, niebieski → 01000 itp. — tzn. wprowadzamy 5 cech dychotomicznych!
		- Nie wprowadzamy kombinacji, np. zielony ↛ 11000. Ale może świadomie chcemy (wtedy kodowanie binarne świetnie się sprawdzi)? 
		- Mieszanie kolorów — może mieć sens, gdy robimy model UM dla astrofizyków. . .
		- Zaleta w stosunku do poprzednich metod: nie narzucamy żadnego porządku.
		- Są też wady: gdy dużo opcji w ramach kategorii
### Analiza zmiennych indywidualnych 

1. Jest to wyznaczenie parametrów statystycznych zmiennych numerycznych:
	- minimum 
	- maksimum
	- rozstęp 
	- dominanta 
	- Wskaźnik tendencji centralnych
		- średnia
		- mediana
	- Wskaźnik rozproszeń
		- wariancja/ odchylenie standardowe
		- medianowe odchylenie bezwzględne
		- skośność
### Analiza relacji między zmiennymi
1. Przedstawiane za pomocą map cieplnych
2. Przykładem może być :
	1. Macierz kowariancji - wskaźnik rozproszenia i zależności
	2. Macierz korelacji

### Postępowanie z elementami odstającymi

1. Wykrywanie:
	- pojedyncza zmienna - proste, bo nie typowo duże małe, dobrze widoczne na wykresach pudełkowych 
	- wiele zmiennych - trudne , używamy różnych metryk odległości, lub analizy regresji 
	- wynikają z nietypowej naturalnej obserwacji
	- błędu pomiarowym
	- błędu w trakcie wprowadzania danych
2. Postępowanie:
	- zazwyczaj się je odrzuca 
	- podmienia na inną wartość 
	- Jednak możemy chcieć pokazać modelowi anomalie w celu wukruwania anomali 

### Inżynieria cech 

1. Wybór cech - redukujemy cechy podobne lub nie potrzebne, szukamy zależności między cechami np. za pomocą PCA
2. Ekstrakcja cech - poszukiwanie zmiennych syntetycznych np. kombinownaie cech ze sobą 
3. Transformacja cech  - przekształcanie w celu zyskania bardziej znaczących danych

