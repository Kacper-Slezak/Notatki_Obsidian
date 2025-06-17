# Analiza implementacji filtrów cyfrowych

W tym dokumencie przedstawiona jest szczegółowa analiza implementacji z dostarczonych plików źródłowych (Zad1.m, Zad3.m, Zad4.m) pod kątem zgodności z wymaganiami z instrukcji laboratoryjnej "Filtry specjalne: Hilberta, różniczkujący, interpolatora, decymatora".

## 1. Filtr Hilberta, demodulacja AM

### Wymagania z instrukcji:

- Wyznaczenie parametrów sygnału modulującego (A₁, A₂, A₃, f₁, f₂, f₃) dla AM
- Wykorzystanie filtru Hilberta (FIR) do przesunięcia fazowego o -π/2
- **Zakaz używania wbudowanej funkcji `hilbert(...)` lub podobnych**
- Opcjonalnie: rekonstrukcja sygnału zmodulowanego i porównanie z oryginalnym

### Implementacja:

```matlab
% Projektowanie filtru Hilberta (przesuwnik fazowy o -π/2)
N = 63; % Długość filtru (musi być nieparzysta)
n = -(N-1)/2:(N-1)/2; % Indeksy próbek
h_ideal = zeros(1, length(n));

% Idealna odpowiedź impulsowa filtru Hilberta
for i = 1:length(n)
    if n(i) ~= 0
        h_ideal(i) = 2/(pi*n(i)) * sin(pi*n(i)/2)^2;
    else
        h_ideal(i) = 0; % W n=0 odpowiedź impulsowa jest zerowa
    end
end

% Zastosowanie okna Hamminga do poprawy charakterystyki filtru
window = hamming(N)';
h = h_ideal .* window;
```

### Ocena zgodności:

✅ **Implementacja poprawna**:

- Prawidłowo zdefiniowano odpowiedź impulsową filtru Hilberta
- Zastosowano okno Hamminga dla poprawy charakterystyki
- Nie używano niedozwolonej funkcji `hilbert()`
- Poprawnie zaimplementowano proces demodulacji AM, obliczając obwiednię jako pierwiastek z sumy kwadratów sygnału i jego transformaty Hilberta
- Część opcjonalna została zrealizowana poprawnie poprzez odtworzenie sygnału AM na podstawie wyznaczonych parametrów

### Obliczanie obwiedni (demodulacja AM):

```matlab
% Filtracja - obliczenie transformaty Hilberta sygnału
x_hilbert = filter(h, 1, x);

% Kompensacja opóźnienia filtru
delay = (N-1)/2;
x_hilbert = x_hilbert(delay+1:end);
x_sync = x(1:end-delay);

% Obliczenie obwiedni - demodulacja AM
envelope = sqrt(x_sync.^2 + x_hilbert.^2);
```

## 2. Filtr interpolatora i decymatora, mikser audio

### Wymagania z instrukcji:

- Połączenie trzech sygnałów o różnych częstotliwościach próbkowania
- Implementacja nadpróbkowania, filtracji interpolującej, filtracji decymującej i decymacji
- Wybranie optymalnego sposobu łączenia sygnałów
- Miksowanie rzeczywistych sygnałów audio do częstotliwości 48 kHz
- Opcjonalnie: repróbkowanie do częstotliwości CD-Audio oraz implementacja alternatywnych metod

### Implementacja repróbkowania sygnału x1:

```matlab
% Współczynnik nadpróbkowania (upsampling)
up_factor1 = fs_target / fs1; % = 6

% Nadpróbkowanie przez wstawienie zer (upsampling)
x1_upsampled = zeros(length(x1) * up_factor1, 1);
x1_upsampled(1:up_factor1:end) = x1;

% Projektowanie filtru interpolującego dla x1
cutoff1 = (fs1/2) / fs_target;
filter_order1 = 48; % Rząd filtru interpolującego 
b_interp1 = fir1(filter_order1, cutoff1, 'low') * up_factor1;

% Filtracja interpolująca
x1_interpolated = filter(b_interp1, 1, x1_upsampled);

% Kompensacja opóźnienia filtru
delay1 = filter_order1 / 2;
x1_interpolated = x1_interpolated(delay1+1:end);
x1_interpolated = [x1_interpolated; zeros(delay1, 1)];
```

### Implementacja repróbkowania ułamkowego dla x2:

```matlab
% Najpierw nadpróbkowanie o czynnik 3
x2_upsampled_3 = zeros(length(x2) * 3, 1);
x2_upsampled_3(1:3:end) = x2;
    
% Filtracja interpolująca
x2_interpolated_3 = filter(b_interp2_up, 1, x2_upsampled_3);
    
% Następnie decymacja o czynnik 2
% Filtracja antyaliasingowa przed decymacją
x2_filtered = filter(b_decim2, 1, x2_interpolated_3);
    
% Decymacja
x2_interpolated = x2_filtered(1:2:end);
```

### Metody alternatywne:

1. **Interpolacja liniowa**:

```matlab
x1_linear = interp1(t1, x1, t_target, 'linear');
```

2. **Rekonstrukcja z funkcją sinc**:

```matlab
sinc_func = @(x) sin(pi*x)./(pi*x + eps);

% Repróbkowanie x1 metodą sin(x)/x
x1_sinc = zeros(size(t_target));
for i = 1:length(t1)
    % Dla każdej próbki oryginalnego sygnału
    t_diff = t_target - t1(i);
    x1_sinc = x1_sinc + x1(i) * sinc_func(fs1 * t_diff);
end
```

### Ocena zgodności:

✅ **Implementacja poprawna**:

- Prawidłowo zaimplementowano nadpróbkowanie przez wstawianie zer
- Poprawnie zaprojektowano filtry interpolacyjne i decymacyjne
- Zastosowano optymalny sposób łączenia sygnałów
- Uwzględniono kompensację opóźnień filtrów
- Zrealizowano miksowanie rzeczywistych sygnałów audio
- Opcjonalne metody repróbkowania zostały poprawnie zaimplementowane

## 3. Filtr różniczkujący, dekodowanie FM

### Wymagania z instrukcji:

- Implementacja 3 metod dekodowania sygnału FM:
    1. Wykorzystanie składowych I(n) i Q(n)
    2. Różniczkowanie z filtrem pasmowo-przepustowym
    3. Kaskada oddzielnych filtrów pasmowo-przepustowego i różniczkującego
- Opcjonalnie: Zaprojektowanie filtru różniczkującego pasmowo-przepustowego za pomocą funkcji `firls()`

### Implementacja filtru różniczkującego:

```matlab
% Idealna odpowiedź impulsowa filtru różniczkującego
for i = 1:length(n_diff)
    if n_diff(i) == 0
        h_diff_ideal(i) = 0;
    else
        h_diff_ideal(i) = (sin(pi*n_diff(i)) - pi*n_diff(i)*cos(pi*n_diff(i))) / (pi*n_diff(i)^2);
    end
end

% Zastosowanie okna Blackmana do poprawy charakterystyki filtru różniczkującego
window_diff = blackman(Ndiff)';
h_diff = h_diff_ideal .* window_diff;
```

### Implementacja kaskady filtrów:

```matlab
% Projektowanie filtru pasmowo-przepustowego
h_bp = fir1(Nbp-1, [f_low, f_high], 'bandpass', blackman(Nbp));

% Obliczenie odpowiedzi impulsowej kaskady filtrów różniczkującego i pasmowo-przepustowego
h_diff_bp = conv(h_diff, h_bp);
```

### Implementacja z wykorzystaniem firls (bonus):

```matlab
% Projektowanie filtru różniczkującego pasmowo-przepustowego
Nbp_diff = 201;
f = [0, f_low-0.01, f_low, f_high, f_high+0.01, 1];
a = [0, 0, 1j, -1j, 0, 0]; % Odpowiedź różniczkująca (mnożenie przez jω)

% Projektowanie filtru za pomocą firls
h_bp_diff = firls(Nbp_diff-1, f, abs(a));

% Konwersja odpowiedzi do rzeczywistej (usunięcie części urojonej)
h_bp_diff = real(h_bp_diff);
```

### Ocena zgodności:

✅ **Implementacja poprawna**:

- Poprawnie zaimplementowano wszystkie trzy metody dekodowania FM
- Prawidłowo zaprojektowano filtr różniczkujący i pasmowo-przepustowy
- Zaimplementowano kaskadę filtrów jako splot ich odpowiedzi impulsowych
- Poprawnie wykonano odzyskiwanie obwiedni przez kwadraturowanie, filtrację i pierwiastkowanie
- Opcjonalnie poprawnie zaimplementowano filtr różniczkujący pasmowo-przepustowy za pomocą funkcji `firls()`

## Podsumowanie

Analiza dostarczonych implementacji wykazuje pełną zgodność z wymaganiami postawionymi w instrukcji laboratoryjnej. Wszystkie zadania zostały zrealizowane poprawnie, bez wykorzystania niedozwolonych funkcji lub uproszczeń. Implementacje wykazują prawidłowe zrozumienie podstaw teoretycznych dotyczących filtrów cyfrowych oraz świadomość skutków praktycznych związanych z ich zastosowaniem.

Szczególnie warte podkreślenia są:

1. **Prawidłowa implementacja filtrów Hilberta** bez korzystania z gotowych funkcji
2. **Poprawna obsługa opóźnień filtrów** w procesie repróbkowania
3. **Efektywna implementacja filtrów FIR** z zastosowaniem okien do poprawy charakterystyk
4. **Poprawna realizacja demodulacji AM i FM**

Wszystkie implementacje są technicznie poprawne i zgodne z teorią przetwarzania sygnałów cyfrowych, co świadczy o dobrym zrozumieniu zagadnień związanych z filtracją cyfrową, interpolacją i decymacją sygnałów.


# Zagadnienia
- Charakterystyka filtru nie lapie się w podstawowy podział
- Filtr Hilberta przesuwnik fazowy +-90
- 3 wykresy modulacjic widma
- dgzie jest wstóga boczna na wykresie gdzienni ema skłądowej nosnej 
- usnac resample osono upsmaple i downsample
- przeorbic filtr interpolujący z filtru low pass 
- Zależy od ilosći próbkowania i low pass uciac i chcemy go powiazac zilościa próbek foltr decymujazy wyamgany przed repróobkowaniem 
- korekcja oóźneiń w filtrze rózniczkującym i filtrze bandpass 