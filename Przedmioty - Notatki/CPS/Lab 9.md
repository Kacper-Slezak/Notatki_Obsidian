# Teoretyczne Wyjaśnienie Filtrów Adaptacyjnych

Przedstawione kody implementują różne zastosowania filtrów adaptacyjnych w cyfrowym przetwarzaniu sygnałów. Filtry adaptacyjne to filtry, które mogą zmieniać swoje parametry (współczynniki) w czasie rzeczywistym, aby dostosować się do zmian w przetwarzanych sygnałach. W tym dokumencie omówię podstawy teoretyczne tych implementacji oraz wyjaśnię działanie każdego z przedstawionych kodów.

## 1. Podstawy filtracji adaptacyjnej

### Filtr FIR i jego rola w filtracji adaptacyjnej

Większość pokazanych implementacji używa filtru FIR (Finite Impulse Response) o skończonej odpowiedzi impulsowej. Filtry te charakteryzują się równaniem:

```
y(n) = h(0)·x(n) + h(1)·x(n-1) + ... + h(M-1)·x(n-M+1)
```

gdzie:

- `y(n)` to sygnał wyjściowy filtru
- `x(n)`, `x(n-1)`, ... to bieżąca i poprzednie próbki sygnału wejściowego
- `h(0)`, `h(1)`, ... to współczynniki filtru (nazywane też wagami)
- `M` to długość filtru (liczba współczynników)

W filtracji adaptacyjnej współczynniki `h` są zmieniane w czasie według określonego algorytmu, aby zminimalizować różnicę między sygnałem wyjściowym filtru a pożądanym sygnałem odniesienia.

### Algorytmy adaptacji

W przedstawionych kodach zaimplementowano trzy główne algorytmy adaptacji współczynników filtru:

1. **LMS (Least Mean Square)** - algorytm, w którym współczynniki są aktualizowane według wzoru:
    
    ```
    h(n+1) = h(n) + μ·e(n)·x(n)
    ```
    
    gdzie:
    
    - `μ` (mu) to współczynnik szybkości adaptacji
    - `e(n)` to błąd, czyli różnica między sygnałem odniesienia a wyjściem filtru
    - `x(n)` to wektor próbek wejściowych (bufor)
2. **NLMS (Normalized LMS)** - normalizowana wersja LMS, w której współczynnik adaptacji jest dzielony przez energię sygnału wejściowego:
    
    ```
    h(n+1) = h(n) + μ·e(n)·x(n) / (γ + x(n)ᵀ·x(n))
    ```
    
    gdzie `γ` to mały współczynnik zapobiegający dzieleniu przez zero przy niskiej energii sygnału.
    
3. **RLS (Recursive Least Squares)** - algorytm wykorzystujący ważoną sumę kwadratów błędów, oferujący szybszą zbieżność, ale bardziej kosztowny obliczeniowo:
    
    ```
    k = (Rinv·x) / (λ + xᵀ·Rinv·x)
    Rinv = (Rinv - k·xᵀ·Rinv) / λ
    h = h + e·k
    ```
    
    gdzie:
    
    - `k` to wektor wzmocnienia Kalmana
    - `Rinv` to odwrotność macierzy korelacji
    - `λ` to współczynnik zapominania (zazwyczaj bliski 1)

## 2. Analiza kodu 1: Filtracja adaptacyjna dla różnych sygnałów

Pierwszy kod (`paste.txt`) demonstruje zastosowanie filtracji adaptacyjnej do odszumiania trzech różnych typów sygnałów:

- sygnał sinusoidalny (suma dwóch sinusoid)
- sygnał z modulacją częstotliwości (SFM)
- nagranie dźwięku silnika

### Teoretyczne wyjaśnienie procesu odszumiania

Układ wykorzystuje adaptacyjny filtr szumu (ANC - Adaptive Noise Cancelling), który wykorzystuje zasadę liniowej predykcji. Kluczowa idea polega na tym, że składowe deterministyczne (np. sinusoidy) można przewidzieć na podstawie poprzednich próbek, podczas gdy szum losowy jest nieprzewidywalny.

W tym konkretnym układzie:

- Sygnał odniesienia `d` to zaszumiony sygnał
- Sygnał wejściowy `x` do filtru to ten sam sygnał, ale opóźniony o jedną próbkę
- Filtr adaptacyjny "uczy się" przewidywać sygnał na podstawie poprzednich próbek
- Składowe deterministyczne (sinusoidy) są dobrze przewidywane i pozostają w sygnale
- Składowe szumowe (losowe) są słabo przewidywalne i zostają wyeliminowane

Dla różnych SNR (stosunku sygnału do szumu) układ działa z różną skutecznością. Wykresy w kodzie pokazują:

- Oryginalny sygnał (przed dodaniem szumu)
- Sygnał z dodanym szumem (o różnych poziomach SNR - 10, 20, 40 dB)
- Sygnał po filtracji (odszumiony)

Dla każdego typu sygnału i każdego poziomu SNR obliczany jest wynikowy SNR, który pokazuje skuteczność odszumiania.

## 3. Analiza kodu 2: Kasowanie echa w zestawie telekonferencyjnym

Drugi kod (`paste-2.txt`) implementuje układ kasowania echa w zestawie telekonferencyjnym. Jest to typowy problem w systemach telekonferencyjnych, gdzie mikrofon odbiera zarówno głos lokalnego użytkownika, jak i echo sygnału z głośnika.

### Teoretyczne wyjaśnienie kasowania echa

W układzie kasowania echa:

- `s_a` to sygnał mowy użytkownika A (oryginalny, bez echa)
- `s_b` to sygnał mowy użytkownika B (wejście do głośnika)
- `s_combined` to sygnał z mikrofonu zawierający mowę A oraz echo sygnału B

Układ adaptacyjny działa następująco:

1. Filtr adaptacyjny przyjmuje sygnał `s_b` jako wejście
2. Na wyjściu filtru otrzymuje się estymację echa `G(s_b)`
3. Estymowane echo jest odejmowane od sygnału z mikrofonu, dając estymację czystego sygnału użytkownika A

Kluczowy element to filtr adaptacyjny, który "uczy się" odtwarzać charakterystykę kanału echo (G) między głośnikiem a mikrofonem. Kiedy filtr dokładnie modeluje ten kanał, może generować dokładną replikę echa, która po odjęciu od sygnału mikrofonu pozostawia czysty sygnał użytkownika A.

W tym kodzie zaimplementowano trzy różne algorytmy adaptacji:

- LMS (Least Mean Square)
- NLMS (Normalized LMS)
- RLS (Recursive Least Squares)

Skuteczność kasowania echa jest mierzona za pomocą:

- SNR wejściowego i wyjściowego
- Poprawy SNR
- MSE (błędu średnokwadratowego)

## 4. Analiza kodu 3: Cyfrowa pętla PLL dla pilota 19 kHz

Trzeci kod (`paste-3.txt`) implementuje cyfrową pętlę synchronizacji fazowej (PLL - Phase-Locked Loop) dla pilota 19 kHz, który jest używany w stereofonicznej transmisji FM.

### Teoretyczne wyjaśnienie działania PLL

Pętla PLL jest systemem sprzężenia zwrotnego, który automatycznie dostosowuje fazę i częstotliwość generowanego sygnału, aby zsynchronizować go z sygnałem wejściowym (pilotem). Podstawowe komponenty cyfrowej PLL to:

1. **Detektor fazy** - wykrywa różnicę fazową między sygnałem wejściowym a generowanym:
    
    ```
    perr = -p(n)*sin(theta(n))
    ```
    
2. **Filtr pętli** - wygładza sygnał błędu fazowego, zapobiegając gwałtownym zmianom:
    
    ```
    theta(n+1) = theta(n) + freq + alpha*perr
    freq = freq + beta*perr
    ```
    
    gdzie:
    
    - `alpha` kontroluje korektę fazy
    - `beta` kontroluje korektę częstotliwości
    - `freq` to bieżąca estymacja częstotliwości kątowej
3. **Oscylator sterowany numerycznie (NCO)** - generuje sygnał wyjściowy o częstotliwości i fazie kontrolowanej przez filtr pętli:
    
    ```
    cos(theta(n))
    ```
    

Kod testuje PLL w trzech scenariuszach:

1. Dla syntetycznego pilota 19 kHz z stałym przesunięciem fazowym
2. Dla pilota z modulacją częstotliwości (±10 Hz, fm=0.1 Hz)
3. Dla pilota z różnymi poziomami SNR, aby zbadać szybkość synchronizacji

Kluczowym aspektem PLL jest zdolność do śledzenia zmian częstotliwości i fazy sygnału wejściowego, co jest istotne w systemach komunikacyjnych, gdzie częstotliwość nośna może ulegać drobnym fluktuacjom.

## 5. Zastosowania filtrów adaptacyjnych

Na podstawie analizowanych kodów i dokumentacji z laboratorium, można wyodrębnić kilka kluczowych zastosowań filtrów adaptacyjnych:

### 5.1. Odszumianie (ANC - Adaptive Noise Cancelling)

- **Jak działa**: Filtr adaptacyjny "uczy się" odróżniać składowe deterministyczne (sygnał) od losowych (szum)
- **Zastosowania**: Poprawa jakości sygnałów audio, przetwarzanie mowy, systemy komunikacyjne

### 5.2. Kasowanie echa (Echo Cancellation)

- **Jak działa**: Filtr adaptacyjny modeluje ścieżkę echa i generuje jego replikę do odejmowania
- **Zastosowania**: Systemy telekonferencyjne, zestawy głośnomówiące, telefonia VoIP

### 5.3. Identyfikacja obiektu (System Identification)

- **Jak działa**: Filtr adaptacyjny uczy się modelować charakterystykę nieznanego systemu
- **Zastosowania**: Identyfikacja kanałów komunikacyjnych, modelowanie akustyki pomieszczeń

### 5.4. Synchronizacja fazowa (PLL)

- **Jak działa**: System sprzężenia zwrotnego dostosowuje fazę i częstotliwość oscylatora
- **Zastosowania**: Odbiór sygnałów radiowych, dekodowanie stereo FM, odtwarzanie zegara w komunikacji cyfrowej

### 5.5. Usuwanie zakłóceń w sygnałach biomedycznych

- **Jak działa**: Filtr adaptacyjny eliminuje zakłócenia sieciowe (50/60 Hz) i szum mięśniowy
- **Zastosowania**: Przetwarzanie sygnałów EKG, EEG i innych sygnałów biomedycznych

## 6. Podsumowanie algorytmów adaptacji

### 6.1. LMS (Least Mean Square)

- **Zalety**: Prostota implementacji, niska złożoność obliczeniowa
- **Wady**: Wolniejsza zbieżność, wrażliwość na rozpiętość wartości własnych macierzy korelacji sygnału wejściowego
- **Zastosowania**: Systemy o ograniczonych zasobach obliczeniowych

### 6.2. NLMS (Normalized LMS)

- **Zalety**: Lepsza stabilność, adaptacja współczynnika uczenia do energii sygnału
- **Wady**: Nieco większa złożoność obliczeniowa niż LMS
- **Zastosowania**: Przetwarzanie sygnałów o zmiennej mocy

### 6.3. RLS (Recursive Least Squares)

- **Zalety**: Szybsza zbieżność, lepsza dokładność, mniejsza wrażliwość na rozpiętość wartości własnych
- **Wady**: Większa złożoność obliczeniowa, wymagania pamięciowe
- **Zastosowania**: Systemy wymagające szybkiej adaptacji, systemy z wystarczającą mocą obliczeniową

## Podsumowanie

Filtry adaptacyjne są potężnym narzędziem w cyfrowym przetwarzaniu sygnałów, zdolnym do dynamicznego dostosowywania się do zmiennych warunków. Przedstawione kody demonstrują różnorodne zastosowania tych filtrów w praktyce, od odszumiania i kasowania echa po synchronizację fazową i identyfikację systemów.

Kluczowym elementem w projektowaniu filtrów adaptacyjnych jest wybór odpowiedniego algorytmu adaptacji oraz staranny dobór parametrów, takich jak długość filtru, współczynnik adaptacji i inne specyficzne dla danego algorytmu. Wybór ten zależy od konkretnego zastosowania, wymagań dotyczących szybkości zbieżności, stabilności i złożoności obliczeniowej.



