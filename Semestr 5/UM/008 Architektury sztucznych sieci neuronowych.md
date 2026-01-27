# Rodzaje architektur:

- Sieci splotowe
- Sieci rekursyjne

## Perceptor wielowarstwowy :

- Regresja 
- Klastyfikacja
- Działa na liczbach

## Sieci splotowe CNN:
	convolutional networks
	sieci-splotowe

- zakłada się że dane wejściowe mają regularną strukturę i kluczowe jest wykrycie wzorców 
- sieci które samodzielnie wykrywają cechy ( rzucamy na sieci wektor np. zdjęcia, i sieć musi wykryć cechy )
- dobrze sobie radzą z przeskalowaniem danych, przesunięciem cech obrazowych 
- podobieństwo do klasycznych sieci neuronowych opartych o perceptron wielowarstwowy:
	- używają neuronów uczących się, występują funkcje aktywacji
- różnice w stosunku do klasycznego:
	- kluczowe jest użycie operacji splotu(przekształcenie linowe) - służy do filtrowania danych - cel wykrywanie wzorców
	- dostajemy sygnały przetwarzane są one przez wagi i czasem dodaje bias
	- zamiast mnożenia macierzowo-wektorowego używamy splotu 
	- łatwiejsza implementacja obliczeń, redukcja parametrów sieci dzięki ich uwspólnieniu
	- oszczędzamy na ilości wag, więcej wag -> przeuczenie, 
- architektura i sposób działania:
	- nie stosujemy osobnych wag dla każdego piksela tylko wykorzystujemy te same wagi dla całego obrazu jeździmy po obrazie (filtrujemy)
	- dokonuje się [[Pooling]] - agregacja
	- budujemy wektor w pewnym sensie cech
	- na koniec z wektora korzystamy z perceptrona wielowarstwowego 
	- [[warstwa splotowa]]
- Splot :
	- ciągły 
	- dyskretny - suma wejścia razy waga( wytrenowana )
	- Cechy:
		- jest przemienny
		- stosujemy odwrócenie
- Hiper parametry warstwy splotowej:
	- padding - np. dopełnienie sztuczne obrazu 0 
	- spride

# Sieci Rekurencyjne RNN

- analiza szeregów czasowych 
- ma pamięć poprzednią tego co zobaczyła 
- różne możliwości konstrukcji 
	- np. jednokierunkowe
- propagacja wsteczna w czasie 
#### Wady:

- 