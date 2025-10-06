
## Cyfrowe Przetwarzanie Sygnałów: Kompresja Dźwięku

### Zadanie 1: Koder dźwięku DPCM

**Teoria:**

DPCM (Differential Pulse Code Modulation) to technika kompresji danych, która wykorzystuje redundancję w sygnale audio. Zamiast kodować każdą próbkę sygnału niezależnie (jak w PCM), DPCM koduje różnicę między bieżącą próbką a przewidywaną wartością tej próbki. Przewidywanie jest oparte na poprzednich próbkach sygnału. W tym zadaniu predykcja jest bardzo prosta: a⋅x(n−1), gdzie a to współczynnik predykcji.

**Schemat DPCM:**

- **Koder:**
    1. **Predykcja:** Oblicza się przewidywaną wartość bieżącej próbki (a⋅x(n−1)).
    2. **Różnica (błąd predykcji):** Różnica d(n)=x(n)−a⋅x(n−1) jest obliczana. Jest to błąd, który należy skwantyzować.
    3. **Kwantyzacja:** Sygnał błędu d(n) jest kwantyzowany do dq(n) (np. do 16 stanów, czyli 4 bity). Kwantyzacja redukuje liczbę bitów potrzebnych do reprezentacji sygnału, ale wprowadza błąd kwantyzacji.
    4. **Rekonstrukcja w koderze:** Aby koder mógł poprawnie wygenerować y(n−1) dla kolejnej próbki, musi zrekonstruować sygnał na podstawie skwantyzowanego błędu: y(n)=dq(n)+a⋅y(n−1). Jest to kluczowe, aby koder i dekoder używały tej samej (potencjalnie zniekształconej przez kwantyzację) wersji sygnału do predykcji, zapobiegając kumulacji błędów.
- **Dekoder:**
    1. Odbiera skwantyzowany sygnał błędu dq(n).
    2. Wykorzystuje tę samą formułę rekurencyjną co koder do rekonstrukcji sygnału: y(n)=dq(n)+a⋅y(n−1).

**Dlaczego to działa?**

Sygnały audio często mają dużą korelację między sąsiednimi próbkami. Oznacza to, że bieżąca próbka jest często bardzo podobna do poprzedniej. Kodując różnicę (błąd predykcji), zamiast samej próbki, uzyskujemy sygnał o mniejszej wariancji (mniejszym zakresie wartości). Sygnał o mniejszym zakresie wartości można skwantyzować z mniejszą liczbą bitów, uzyskując tę samą jakość percepcji, lub z tą samą liczbą bitów, uzyskując lepszą jakość.

**Kwantyzacja:**

Kwantyzacja polega na przypisaniu ciągłej wartości sygnału (np. d(n)) do jednej z ograniczonej liczby dyskretnych poziomów. Ograniczenie d(n) do 16 stanów (4 bity) oznacza, że każda próbka dq(n) będzie reprezentowana za pomocą 4 bitów (24=16). Funkcja `lab11_kwant()` musiałaby najpierw znaleźć minimalną i maksymalną wartość w wektorze d, a następnie podzielić ten zakres na 16 równych przedziałów. Każda próbka d(n) byłaby przypisana do środka przedziału, w którym się znajduje.

**W kodzie `Zad1.m`:**

- `x = audioread(...)`: Wczytuje oryginalny sygnał audio.
- `a = 0.9545;`: Współczynnik predykcji. Jest to często optymalizowany parametr.
- `d = x - a*[ 0; x(1:end-1) ];`: Implementacja kodera DPCM dla sygnału różnicowego. Zauważ, że `x(1:end-1)` odpowiada x(n−1), a `[0; ...]` dodaje zero na początku, aby dopasować długość, ponieważ dla pierwszej próbki nie ma poprzedniej.
- `dq = lab11_kwant( d );`: Tutaj ma nastąpić kwantyzacja sygnału różnicowego.
- `y = ...`: To jest miejsce, gdzie należy zaimplementować dekoder DPCM, używając rekurencji `y(n) = dq(n) + a*y(n-1)`. Należy pamiętać o odpowiednim zainicjowaniu `y(1)` (np. y(1)=dq(1) lub y(1)=x(1) dla uproszczenia w pierwszej próbce, choć dla dokładnej rekonstrukcji powinno być y(1)=dq(1) i x(1) w koderze powinno być traktowane jako d(1) skwantyzowane do dq(1)).

**ADPCM (Adaptive Differential Pulse Code Modulation):**

ADPCM idzie o krok dalej niż DPCM. W ADPCM, krok kwantyzacji (rozmiar przedziału kwantyzacji) i/lub współczynniki predykcji są adaptacyjnie zmieniane w czasie, w zależności od charakterystyki sygnału. Dzięki temu ADPCM może lepiej dostosować się do zmieniającej się dynamiki sygnału audio, co prowadzi do lepszej jakości przy niższych przepływnościach bitowych. Standard G.726 to specyficzna implementacja ADPCM dla głosu, oferująca różne przepływności (16, 24, 32, 40 kbit/s).

### Zadanie 2: Transformacyjne kodowanie dźwięku

**Teoria:**

Transformacyjne kodowanie dźwięku polega na przekształceniu sygnału audio z dziedziny czasu do dziedziny częstotliwości (lub innej dziedziny transformaty). W tej nowej dziedzinie energia sygnału jest często skoncentrowana w mniejszej liczbie współczynników. Te "ważniejsze" współczynniki mogą być kwantyzowane z większą precyzją, a "mniej ważne" z mniejszą, lub nawet pominięte, co prowadzi do kompresji.

**MDCT (Modified Discrete Cosine Transform):**

MDCT jest wariantem DCT, specjalnie zaprojektowanym do zastosowań kompresji audio ze względu na swoje właściwości:

	- **Nakładanie się okien (Overlap-Add):** MDCT operuje na nakładających się oknach sygnału. To jest kluczowe dla uniknięcia artefaktów blokowych (słyszalnych "kliknięć" lub "brzęczeń") na granicach ramek, które mogłyby powstać przy prostym podziale sygnału na bloki.
- **Własność Perfect Reconstruction (PR):** Przy zastosowaniu odpowiednich okien analizy i syntezy (w tym przypadku okno sinusoidalne h(n)=sin(Nπ​(n+0.5))) oraz macierzy analizy i syntezy, MDCT zapewnia idealną rekonstrukcję sygnału, jeśli nie ma kwantyzacji. To znaczy, że x(n) = y(n) (lub z pominięciem błędu maszynowego) jeśli nie ma strat.
- **Redukcja redundancji:** MDCT przetwarza N próbek wejściowych na N/2 współczynników transformaty, co jest korzystne dla kompresji.

**Kluczowe elementy MDCT:**

- **Okno analizy h(n):** Stosowane do sygnału przed transformacją, aby zmniejszyć efekty obcinania bloku i poprawić właściwości widmowe.
- **Macierz analizy A:** Wykonuje transformację MDCT, przekształcając blok sygnału czasowego na współczynniki w dziedzinie transformaty.
- **Macierz syntezy S:** Wykonuje odwrotną transformatę MDCT, przekształcając współczynniki z powrotem na sygnał czasowy. W przypadku MDCT, S=AT (transpozycja macierzy analizy).
- **Rekonstrukcja z nakładających się okien:** Po transformacji, każdy blok sygnału jest syntetyzowany. Fragmenty syntetyzowanych bloków, które się nakładają, są sumowane, aby odtworzyć ciągły sygnał.

**Zadanie 2 w kontekście kodu `Zad2.m`:**

- `get_mdct_analysis_matrix(N)` i `get_mdct_synthesis_matrix(N)`: Te funkcje generują odpowiednie macierze dla MDCT. Warto zauważyć, że S jest transpozycją A.
- `apply_analysis_window(N)`: Generuje okno sinusoidalne.
- `encode_mdct` i `decode_mdct`: Te funkcje wykonują właściwe kodowanie i dekodowanie.
    - **Kodowanie:**
        1. Sygnał wejściowy jest dzielony na ramki (bloki o długości N).
        2. Do każdej ramki stosowane jest okno analizy.
        3. Zokienkowana ramka jest przekształcana za pomocą macierzy analizy A.
        4. Uzyskane współczynniki MDCT są kwantyzowane (funkcja `encode_mdct` przyjmuje parametr `Q` dla kwantyzacji).
    - **Dekodowanie:**
        1. Skwantyzowane współczynniki MDCT są przetwarzane przez macierz syntezy S.
        2. Do zrekonstruowanego bloku stosowane jest okno syntezy (które jest takie samo jak okno analizy w przypadku sinusoidalnego okna i PR).
        3. Nakładające się części są dodawane (overlap-add), aby odtworzyć sygnał.

**Kluczowe zagadnienia do zrealizowania:**

1. **Różne N (32 i 128):** Parametr N (rozmiar ramki/okna) ma wpływ na charakterystykę kompresji. Krótsze okna (N=32) są lepsze do przetwarzania szybkich zmian w sygnale (np. szumy impulsowe), podczas gdy dłuższe okna (N=128) są lepsze dla sygnałów tonalnych, zapewniając lepszą rozdzielczość częstotliwościową.
2. **Bezstratność:** Koncepcja bezstratności (lub quasi-bezstratności) dla MDCT. Przy braku kwantyzacji (lub bardzo małym Q), MDCT jest bliska bezstratnej.
3. **Przepływność 64 kbps:** Aby uzyskać docelową przepływność, należy obliczyć, ile bitów na współczynnik MDCT jest dozwolone.
    - Częstotliwość próbkowania Fs=44100 Hz.
    - Docelowa przepływność R=64⋅103 bity/sekundę.
    - Liczba współczynników MDCT na ramkę to N/2.
    - Liczba ramek na sekundę to Fs/(N/2) (dla 50% overlap).
    - Jeśli mamy b bitów na współczynnik, to przepływność będzie (N/2)⋅b⋅(Fs/(N/2))=b⋅Fs. To jest uproszczenie, zakładające, że każdy współczynnik jest kodowany niezależnie i nie uwzględnia overheadu (np. nagłówków ramki). Bardziej precyzyjnie, przepływność to R=(liczba bitoˊw na ramkę)⋅(liczba ramek na sekundę). Liczba bitów na ramkę = (N/2)⋅b. Liczba ramek na sekundę zależy od N i stopnia nakładania się. Dla MDCT z 50% nakładaniem, efektywny krok czasowy to N/2. Więc liczba ramek na sekundę to Fs/(N/2). Zatem R=b⋅(N/2)⋅(Fs/(N/2))=b⋅Fs. To sugeruje, że liczba bitów na próbkę b jest stała niezależnie od N. To jest jednak duże uproszczenie.
    - Prawdopodobnie oczekiwane jest, że przepływność 64kbps oznacza efektywną liczbę bitów na próbkę PCM. Jeśli sygnał ma Fs próbek na sekundę i B bitów na próbkę, to pierwotna przepływność to Fs⋅B. Jeśli chcemy Rcel​=64kbps, to musimy zredukować liczbę bitów na próbkę.
    - W kontekście MDCT, jeśli ramka ma N/2 współczynników i przetwarzamy N/2 nowych próbek co ramkę (50% overlap), to możemy obliczyć średnią liczbę bitów na współczynnik.
        - Przepływność = (liczba bitów na ramkę MDCT) / (czas trwania ramki efektywny).
        - Czas trwania ramki efektywny = N/2/Fs.
        - Liczba bitów na ramkę MDCT = (liczba wspoˊłczynnikoˊw)⋅(liczba bitoˊw na wspoˊłczynnik)=(N/2)⋅b.
        - Rcel​=((N/2)⋅b)/(N/2/Fs)=b⋅Fs.
        - Zatem b=Rcel​/Fs. Jeśli Rcel​=64000 bity/s i Fs=44100 Hz, to b=64000/44100≈1.45 bitów/próbkę. To oznacza, że średnio każdy współczynnik MDCT może być reprezentowany za pomocą około 1.45 bita. To wymaga użycia kwantyzacji niejednolitej lub alokacji bitów, gdzie niektóre współczynniki dostają więcej bitów, a inne mniej.
4. **Dynamiczna alokacja bitów (opcjonalnie):** To zaawansowana technika. Zamiast stałej liczby bitów na współczynnik, można analizować energię lub amplitudę współczynników w każdej ramce. Im większa energia/amplituda, tym więcej bitów jest alokowanych do tego współczynnika. Informacja o alokacji bitów musi być również przesłana do dekodera.
5. **Przejściowe okna (opcjonalnie):** Zmiana długości okna MDCT w trakcie odtwarzania może prowadzić do artefaktów. Okna przejściowe są specjalnie zaprojektowane, aby umożliwić płynną zmianę długości okna bez wprowadzania zniekształceń.

### Zadanie 3: Podpasmowe kodowanie dźwięku

**Teoria:**

Podpasmowe kodowanie dźwięku (Subband Coding) to kolejna technika kompresji, która dzieli sygnał audio na kilka niezależnych pasm częstotliwości (podpasm). Każde podpasmo jest następnie przetwarzane (kwantyzowane i kodowane) niezależnie. Jest to korzystne, ponieważ:

- **Maskowanie psychoakustyczne:** Ucho ludzkie jest mniej wrażliwe na szum w obecności silnych sygnałów w bliskich częstotliwościach. Dzieląc sygnał na podpasma, możemy wykorzystać to zjawisko, alokując mniej bitów do podpasm, gdzie szum będzie maskowany przez inne dźwięki.
- **Różna percepcja szumu:** Ucho ludzkie ma różną czułość na szum w różnych pasmach częstotliwości (np. jest mniej wrażliwe na wysokie częstotliwości). Możemy kwantyzować podpasma w sposób dostosowany do tej wrażliwości.
- **Redukcja redundancji:** Energia sygnału nie jest równomiernie rozłożona w całym paśmie częstotliwości. Niektóre podpasma mogą zawierać bardzo mało energii, a zatem mogą być kwantyzowane z mniejszą liczbą bitów lub nawet całkowicie pominięte.

**Schemat (uproszczony):**

1. **Filtracja:** Sygnał wejściowy jest przepuszczany przez zestaw filtrów pasmowoprzepustowych, dzieląc go na M podpasm.
2. **Decymacja:** Sygnał w każdym podpaśmie jest próbkowany z niższą częstotliwością, odpowiadającą szerokości pasma.
3. **Kwantyzacja:** Próbki w każdym podpaśmie są kwantyzowane. Liczba bitów użyta do kwantyzacji może być stała dla wszystkich podpasm lub dynamicznie alokowana.
4. **Kodowanie:** Skwantyzowane próbki są kodowane (np. za pomocą kodowania entropijnego, jak Huffman).
5. **Dekodowanie:** Odwrotny proces: dekodowanie, dekwantyzacja, interpolacja (upsampling) i synteza z powrotem w pełnopasmowy sygnał.

**Zadanie 3 w kontekście kodu `Zad3.m`:**

- **`kodowanie_podpasmowe.m`:** Jest to zewnętrzna funkcja, która prawdopodobnie implementuje podstawowy koder/dekoder podpasmowy.
- **Liczba podpasm (8, 32):** Wpływa na rozdzielczość częstotliwościową i zdolność do wykorzystania zjawisk psychoakustycznych. Więcej podpasm oznacza lepszą granularność.
- **Stała liczba bitów (6 bitów na podpasmo):** Prosty schemat kwantyzacji, gdzie każde podpasmo otrzymuje taką samą liczbę bitów.
- **Zmienna liczba bitów (np. 8, 8, 7, 6, (4)):** To bardziej zaawansowana technika. Bitów alokuje się więcej dla podpasm o większej energii lub tam, gdzie ucho ludzkie jest bardziej wrażliwe. Pozostałe podpasma dostają mniej bitów.
- **Spektrogram:** Jest to wizualna reprezentacja sygnału audio w dziedzinie czasu i częstotliwości. Pozwala ocenić jakość kompresji, obserwując, gdzie występują zniekształcenia (np. rozmycie szumów, utrata detali tonalnych).
- **Błąd kodowania i SNR:** SNR (Signal-to-Noise Ratio) to miara jakości rekonstrukcji. Wyższy SNR oznacza mniejszy błąd.
- **Dynamiczna alokacja bitów (0.75 pkt):** To jest kluczowy element tego zadania. Alokacja bitów na podstawie energii sygnału w danym podpaśmie. Im większa energia, tym więcej bitów. Informacja o alokacji bitów musi być przesłana do dekodera, co jest dodatkowym narzutem (overhead), ale niezbędnym.

### Zadanie 4: Szacowanie ilości informacji – Entropia

**Teoria:**

Entropia Shannona H(X) jest miarą średniej ilości informacji (lub niepewności) zawartej w symbolu źródła. Jest ona fundamentalną koncepcją w teorii informacji i stanowi dolną granicę dla średniej liczby bitów potrzebnych do bezstratnego zakodowania symbolu ze źródła.

Wzór na entropię:

H(x)=−∑n=1N​pn​log2​pn​

Gdzie:

- N: liczba unikalnych symboli w ciągu.
- pn​: prawdopodobieństwo wystąpienia n-tego unikalnego symbolu.
- log2​: logarytm o podstawie 2, ponieważ jednostką informacji jest bit.

**Znaczenie:**

Niższa entropia oznacza, że sygnał jest bardziej przewidywalny (ma więcej redundancji), a zatem może być bardziej efektywnie skompresowany. Wyższa entropia oznacza większą losowość i mniej możliwości kompresji.

**Zadanie 4 w kontekście kodu `Zad4.m`:**

- `calculate_entropy(x)`: Funkcja ta przyjmuje ciąg symboli `x` i oblicza jego entropię.
    1. `unique_symbols = unique(x);`: Znajduje wszystkie unikalne wartości w ciągu.
    2. `probabilities = zeros(size(unique_symbols));`: Inicjuje wektor do przechowywania prawdopodobieństw.
    3. Pętla `for i = 1:length(unique_symbols)`: Oblicza prawdopodobieństwo wystąpienia każdego unikalnego symbolu jako `(liczba wystąpień symbolu) / (całkowita liczba symboli)`.
    4. `H = -sum(probabilities .* log2(probabilities));`: Stosuje wzór Shannona do obliczenia entropii.
- Testowe sygnały `x1`, `x2`, `x3`: Te sekwencje służą do sprawdzenia poprawności implementacji funkcji `calculate_entropy` i zrozumienia, jak różne rozkłady symboli wpływają na entropię.
    - `x1` ma rozkład symetryczny.
    - `x2` ma symbole o różnej częstotliwości występowania.
    - `x3` jest bardzo nierównomierny (prawie wszystkie zera, jedno 15), co powinno dać niską entropię.

### Zadanie 5: Koder Huffmana

**Teoria:**

Kodowanie Huffmana to algorytm kompresji danych bezstratnej, oparty na zmiennej długości słów kodowych (VLC - Variable Length Coding). Przypisuje krótsze słowa kodowe (sekwencje bitów) symbolom, które występują częściej, i dłuższe słowa kodowe symbolom rzadszym. Celem jest minimalizacja średniej długości słowa kodowego, co prowadzi do efektywnej kompresji.

**Kroki budowy drzewa Huffmana:**

1. **Oblicz prawdopodobieństwa:** Dla każdego unikalnego symbolu w danych wejściowych oblicz jego prawdopodobieństwo wystąpienia.
2. **Utwórz liście:** Każdy symbol staje się liściem w drzewie, z przypisanym prawdopodobieństwem.
3. **Połącz najmniejsze:** W każdym kroku połącz dwa węzły (lub liście) o najmniejszych prawdopodobieństwach w nowy węzeł. Prawdopodobieństwo nowego węzła jest sumą prawdopodobieństw jego dzieci.
4. **Kontynuuj:** Powtarzaj krok 3, aż zostanie tylko jeden węzeł (korzeń drzewa).
5. **Przypisz kody:** Przypisz bity (np. 0 dla lewej gałęzi, 1 dla prawej) wzdłuż ścieżek od korzenia do każdego liścia. Sekwencja bitów na ścieżce do liścia staje się słowem kodowym dla danego symbolu.

**Właściwości kodowania Huffmana:**

- **Bezstratne:** Dekodowanie jest dokładne, oryginalne dane mogą być perfekcyjnie odtworzone.
- **Prefix codes:** Żaden kod nie jest prefiksem innego kodu, co pozwala na jednoznaczne dekodowanie bez potrzeby specjalnych separatorów.

**Zadanie 5 w kontekście kodu `Zad5v2.m`:**

- `calculate_entropy(x)`: Ponownie używana jest funkcja z zadania 4 do obliczenia entropii, co pozwala porównać teoretyczną granicę kompresji z praktycznym wynikiem Huffmana.
- **Testowe sekwencje:** `x1`, `x2`, `x3`, `x4` są używane do demonstracji i testowania.
- **Ręcznie zbudowane tablice (książki kodowe):** Na początek, zadanie sugeruje ręczne zbudowanie tablic mapujących symbole na kody bitowe i odwrotnie. To pomaga zrozumieć proces.
- **Automatyczne budowanie tablic (opcjonalnie):** To jest bardziej zaawansowana część. Wymaga zaimplementowania algorytmu budowania drzewa Huffmana.
    - `HuffmanNode` i `HuffmanTree` (prawdopodobnie struktury danych w MATLABie, o ile nie są to obiekty, mogą być to struktury zagnieżdżone lub komórki reprezentujące drzewo).
    - `build_huffman_tree`: Funkcja ta powinna przyjmować symbole i ich prawdopodobieństwa/częstotliwości, a następnie iteracyjnie budować drzewo, łącząc najmniejsze węzły.
    - `generate_huffman_codes`: Funkcja, która przechodzi przez zbudowane drzewo i przypisuje słowa kodowe każdemu symbolowi.
    - `huffman_encode`: Funkcja, która przyjmuje sekwencję symboli i używa tablicy kodowej do generowania ciągu bitów.
    - `huffman_decode`: Funkcja, która przyjmuje ciąg bitów i drzewo Huffmana (lub tablicę dekodującą) do odtworzenia oryginalnej sekwencji symboli.
- **Porównanie z entropią:** Bardzo ważne jest porównanie długości zakodowanego sygnału Huffmanem z wynikiem entropii. Długość kodu Huffmana powinna być bliska entropii pomnożonej przez liczbę symboli, ale nigdy mniejsza niż entropia.
- **Błąd pojedynczego bitu:** To jest test wrażliwości kodowania Huffmana na błędy transmisji. Ponieważ kody Huffmana są kodami prefiksowymi, pojedynczy błąd może spowodować błędne zdekodowanie wielu kolejnych symboli, co jest wadą w porównaniu do kodów blokowych.

### Zadanie 6: Analiza-modyfikacja-synteza dźwięku z użyciem MDCT – separacja dźwięków

**Teoria:**

To zadanie wykorzystuje możliwości transformaty MDCT do separacji źródeł dźwięku. Idea opiera się na tym, że różne źródła dźwięku mają często charakterystyczne wzorce w dziedzinie czasowo-częstotliwościowej (spektrogramie). Jeśli potrafimy zidentyfikować te wzorce, możemy selektywnie modyfikować współczynniki MDCT, aby "wyciąć" lub "wzmocnić" konkretne źródło.

**Proces Analiza-Modyfikacja-Synteza (AMS):**

1. **Analiza (Transformacja):** Sygnał audio (miks wielu źródeł) jest dzielony na krótkie, nakładające się ramki. Każda ramka jest transformowana za pomocą MDCT, co daje macierz współczynników MDCT (odpowiednik spektrogramu).
2. **Modyfikacja (Maskowanie):** To jest kluczowy etap separacji. W macierzy współczynników MDCT, dla każdego punktu czasowo-częstotliwościowego (komórki macierzy), można zastosować "maskę".
    - **Maska 0/1:** Jeśli chcemy usunąć dany element częstotliwościowy w danym czasie (związany z niechcianym źródłem), odpowiadający mu współczynnik MDCT jest zerowany (maska 0). Jeśli chcemy zachować element (związany z pożądanym źródłem), współczynnik jest pozostawiony bez zmian (maska 1).
    - **Filtracja w dziedzinie TF:** Można wizualizować spektrogram, identyfikować wzorce poszczególnych sygnałów (np. "skaczące" częstotliwości kanarka), a następnie tworzyć maski, które izolują te wzorce.
3. **Synteza (Odwrotna transformacja):** Zmodyfikowane współczynniki MDCT są następnie przetwarzane odwrotną transformatą MDCT (dekodowanie), a zrekonstruowane ramki są sumowane z nakładaniem się, aby odtworzyć sygnał czasowy.

**Dlaczego MDCT jest lepsze niż FFT/DCT dla tego zadania?**

- **Płynne łączenie ramek:** Dzięki nakładającym się oknom i właściwości Perfect Reconstruction (PR) MDCT pozwala na bardzo płynne łączenie zrekonstruowanych ramek bez artefaktów.
- **Lepsza rozdzielczość TF dla niektórych sygnałów:** Dla sygnałów o szybko zmieniających się częstotliwościach (jak ptak), MDCT może lepiej uchwycić ich charakterystykę niż standardowe FFT dla całego sygnału. Maskowanie może być bardziej precyzyjne w dziedzinie MDCT.

**Zadanie 6 w kontekście kodu `Zad6.m`:**

- **Wczytanie i miksowanie sygnałów:** Dwa sygnały (`KAK.wav` - ptak, `STREET.wav` - ulica/telefon) są wczytywane, resamplowane, konwertowane do mono i miksowane z różnymi wagami, aby stworzyć sygnał wejściowy `x`.
- **Parametry MDCT:** `frame_size` (N), `overlap_ratio` są kluczowe.
- **`MDCT_analysis` i `MDCT_synthesis`:** Funkcje te (założono, że są dostępne lub należy je zaimplementować, podobnie jak w Zadaniu 2) wykonują transformację i odwrotną transformację.
- **Modyfikacja współczynników (maskowanie):** To jest główna część, którą należy zaimplementować. Prawdopodobnie będzie to wyglądało tak:
    1. Obliczenie macierzy współczynników MDCT dla miksu.
    2. Analiza wizualna (np. spektrogramu MDCT, jeśli dostępny) w celu identyfikacji regionów, gdzie występują poszczególne sygnały.
    3. Stworzenie dwóch masek: jednej dla sygnału 1 (ptak) i jednej dla sygnału 2 (telefon). Maski te będą macierzami binarnymi (0 lub 1) o tych samych wymiarach co macierz współczynników MDCT.
    4. Pomnożenie macierzy współczynników MDCT przez każdą maskę, aby uzyskać oddzielone współczynniki dla sygnału 1 i sygnału 2.
    5. Dekodowanie zmodyfikowanych współczynników MDCT z powrotem do sygnałów czasowych (`x_signal1_rec`, `x_signal2_rec`).
- **Obliczanie SNR:** Mierzy jakość separacji, porównując odseparowane sygnały z ich oryginalnymi wersjami.
- **Zapis i odtwarzanie:** Odseparowane sygnały są zapisywane do plików WAV i odtwarzane, co pozwala na subiektywną ocenę jakości separacji.