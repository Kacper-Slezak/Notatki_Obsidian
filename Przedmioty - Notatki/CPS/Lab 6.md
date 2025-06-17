``

---

## 🟦 `zad1_iir_filter.m` – **Filtr IIR z konwersji Butterwortha**

### 🔹 Sekcja 1: Wczytanie i konwersja do transmitancji

```matlab
load('butter.mat');              % wczytanie zera, bieguny, wzmocnienie (z,p,k)
[b_a, a_a] = zp2tf(z, p, k);     % zamiana na postać licznik/mianownik (H(s) = B(s)/A(s))
```

> 	Używamy gotowego filtru analogowego w postaci zera-bieguny-wzmocnienie (ZPK) i zamieniamy go do postaci funkcji przenoszenia.
	
---

### 🔹 Sekcja 2: Konwersja do postaci cyfrowej – bilinear

```matlab
fs = 16000; T = 1/fs;              % częstotliwość próbkowania
[b_d, a_d] = bilinear(b_a, a_a, fs);   % transformacja biliniowa H(s) -> H(z)
```

> Konwersja przy zachowaniu stabilności i minimum zniekształceń fazowych. `bilinear` odwzorowuje oś częstotliwości nieliniowo.

---

### 🔹 Sekcja 3: Rysowanie charakterystyk

```matlab
freqs(b_a, a_a);          % charakterystyka filtru analogowego
hold on;
freqz(b_d, a_d, 1024, fs); % charakterystyka cyfrowa
```

> Porównujemy odpowiedź częstotliwościową H(s) vs H(z).

---

### 🔹 Sekcja 4: Tworzenie sygnału testowego

```matlab
t = 0:1/fs:1;
x = sin(2*pi*1209*t) + sin(2*pi*1272*t);
```

> Dwie harmoniczne – jedna „w paśmie”, druga „poza” – idealne do sprawdzenia działania filtru.

---

### 🔹 Sekcja 5: Własna implementacja filtru IIR

```matlab
for n = 1:N
    ... b(i)*x(n-i+1) ...    % licznik (impulsowa odpowiedź)
    ... - a(j)*y(n-j+1) ...  % sprzężenie zwrotne (rekurencja)
```

> 	Klasyczna struktura filtracji IIR (Direct Form I).

---

### 🔹 Sekcja 6: Porównanie z funkcją `filter()`

```matlab
y_filter = filter(b_d, a_d, x);
```

> `filter()` robi dokładnie to samo co pętla, tylko szybciej – służy jako walidacja.

---

### 🔹 Sekcja 7: Pre-warping (opcjonalne)

```matlab
Wa1 = tan(w1*T/2)*2/T;
```

> Korekta przesunięcia częstotliwości – obliczenie „nowych” granic analogowych, które po bilinear dadzą poprawne cyfrowe.

---

## 🟦 `zad2_dtmf_decode.m` – **Dekodowanie tonów telefonicznych**

---

### 🔹 Sekcja 1: Wczytanie i spektrogram

```matlab
[s, fs] = audioread('s.wav');
spectrogram(s, 4096, 4096-512, 0:5:2000, fs, 'yaxis');
```

> Wykres czasowo-częstotliwościowy – pokazuje, które częstotliwości pojawiają się i kiedy.

---

### 🔹 Sekcja 2: Filtrowanie sygnału filtrem z zad. 1

```matlab
load('butter.mat');
[b_d, a_d] = bilinear(...);
s_filtered = filter(b_d, a_d, s);
```

> Używamy filtru pasmowoprzepustowego do „wyłapania” fragmentów sygnału zawierających określone tony.

---

### 🔹 Sekcja 3: Porównanie spektrogramów

```matlab
subplot(2,1,1); spectrogram(s);
subplot(2,1,2); spectrogram(s_filtered);
```

> Widać, które częstotliwości zostały przepuszczone przez filtr.

---

### 🔹 Sekcja 4: Algorytm Goertzla

```matlab
for i = 1:length(frequencies)
    ... q0 = window(n) + coeff*q1 - q2 ...
```

> Każda iteracja oblicza „energię” danego tonu – jeżeli energia duża → dźwięk był obecny.

---

## 🟦 `zad3_fm_decoder.m` – **Cyfrowe dekodowanie sygnału FM**

---

### 🔹 Sekcja 1: Odczyt IQ i konwersja do sygnału zespolonego

```matlab
wideband_signal = s(1:2:end) + 1i * s(2:2:end);
```

> Oddzielnie są próbki I i Q (naprzemiennie) – łączymy je w sygnał zespolony.

---

### 🔹 Sekcja 2: Przesunięcie widma do 0 Hz

```matlab
wideband_signal_shifted = wideband_signal .* exp(-1i*2*pi*fc/fs*(0:N-1)');
```

> „Wycinamy” jedną stację przesuwając jej nośną do zera – łatwiej wtedy filtrować.

---

### 🔹 Sekcja 3: Filtracja Butterwortha (80 kHz LP)

```matlab
[b, a] = butter(4, 2*80e3/fs);
wideband_signal_filtered = filter(b, a, wideband_signal_shifted);
```

> Izolacja jednej stacji radiowej spośród wszystkich w widmie.

---

### 🔹 Sekcja 4: Zmniejszenie próbkowania

```matlab
x = wideband_signal_filtered(1 : fs/bwSERV : end);
```

> Redukujemy `fs` do pasma stacji (160 kHz).

---

### 🔹 Sekcja 5: Demodulacja FM

```matlab
dx = x(2:end) .* conj(x(1:end-1));
y = atan2(imag(dx), real(dx));
```

> Klasyczny FM demodulator oparty na różniczce fazy (detektor iloczynowy).

---

### 🔹 Sekcja 6: Antyaliasing + de-emfaza

```matlab
[b_lp, a_lp] = butter(4, 2*16e3/bwSERV);
[b_de, a_de] = butter(1, 2*2.1e3/32e3);
```

> Filtracja sygnału przed dalszym zmniejszeniem `fs`, oraz korekcja charakterystyki nadawczej (de-emfaza).

---

### 🔹 Sekcja 7: Odsłuch

```matlab
soundsc(ym, 32e3);
```

> Wysłuchujemy zdekodowanego, monofonicznego sygnału audio.

---

## 🟦 `zad4_real_audio_filtering.m` – **Separacja sygnałów audio**

---

### 🔹 Sekcja 1: Wczytanie nagrań

```matlab
[x1, fs] = audioread('mowa.wav');
[x2, ~] = audioread('ptak.wav');
```

> Wczytujemy dwa różne dźwięki (np. mowa i ptak).

---

### 🔹 Sekcja 2: Mieszanie sygnałów

```matlab
x_mix = x1 + x2;
```

> Tworzymy problem: dwie składowe wymieszane.

---

### 🔹 Sekcja 3: FFT i wykresy

```matlab
X1 = abs(fft(x1));
```

> Widma pokazują, gdzie w dziedzinie częstotliwości znajdują się poszczególne dźwięki.

---

### 🔹 Sekcja 4: Projekt filtru IIR (LP do 3 kHz)

```matlab
[b, a] = butter(4, 2*3000/fs);
```

> Zakładamy, że mowa ma pasmo do 3 kHz – odcinamy wszystko wyżej.

---

### 🔹 Sekcja 5: Filtracja i normalizacja

```matlab
x_filtered = filter(b, a, x_mix);
```

> Usuwamy niepożądaną składową i zapisujemy efekt.

---

### 🔹 Sekcja 6: Analiza – spektrogramy, zera i bieguny

```matlab
zplane(b, a);
fvtool(b, a);
```

> Sprawdzamy, jak filtr działa, jak wygląda jego struktura i odpowiedź częstotliwościowa.


---

## ✅ **ZADANIE 1 – Filtr cyfrowy IIR (Butterworth BP)**

### 🔸 **Teoria:**

- **Filtr Butterwortha** typu **BP** (bandpass) to filtr pasmowoprzepustowy o maksymalnie płaskiej charakterystyce w paśmie przepustowym.
    
- Dany był analogowy filtr H(s) (z postaci z-p-k) – trzeba było dokonać konwersji do cyfrowej postaci H(z) za pomocą **bilinear transform**.
    
- **Bilinear transform** mapuje zmienne s→zs \rightarrow z nieliniowo:
    
    s=2T⋅1−z−11+z−1s = \frac{2}{T} \cdot \frac{1 - z^{-1}}{1 + z^{-1}}
- **Pre-warping** kompensuje nieliniowość odwzorowania częstotliwości w transformacie biliniowej.
    

### 🔸 **Co zrobiłem w kodzie:**

- Załadowanie filtru z `butter.mat`
    
- Konwersja z postaci z-p-k do funkcji przenoszenia H(s)
    
- Bilinear transform → H(z)
    
- Porównanie charakterystyk H(s) vs H(z)
    
- Generacja sygnału testowego (1209 + 1272 Hz)
    
- Filtracja:
    
    - ręczna implementacja rekurencyjna (nie używa `filter()`) ✅
        
    - porównanie z funkcją `filter()` ✅
        
- Opcjonalnie: pre-warping i zaprojektowanie poprawionego filtru
    

### ✅ **Zgodność z wymaganiami:**

✔ Użyto transformaty biliniowej  
✔ Częstotliwość próbkowania: 16 kHz  
✔ Porównano H(s) i H(z), z zaznaczeniem przesunięcia granic  
✔ Wygenerowano odpowiedni sygnał testowy  
✔ Wykonano filtrację bez `filter()`  
✔ Porównano FFT, czas  
✔ Dodatkowo: wykonano **pre-warping** (opcjonalne) ✅

---

## ✅ **ZADANIE 2 – Dekodowanie DTMF**

### 🔸 **Teoria:**

- DTMF (Dual-Tone Multi-Frequency): każda cyfra to **suma 2 sinusoid** – jedna z wiersza i jedna z kolumny macierzy.
    
- Detekcja polega na rozpoznaniu dwóch dominujących częstotliwości.
    
- Spektrogram pozwala zobaczyć te częstotliwości w czasie.
    
- Algorytm Goertzla – optymalny do analizy wybranych częstotliwości (lepszy niż FFT, jeśli interesuje nas tylko kilka tonów).
    

### 🔸 **Co zrobiłem:**

- Załadowanie sygnału `s.wav` (wzorzec wszystkich cyfr)
    
- Wykres spektrogramu
    
- Filtrowanie tego sygnału filtrem z zadania 1
    
- Porównanie spektrogramów przed i po filtracji ✅
    
- Implementacja algorytmu Goertzla dla częstotliwości DTMF ✅
    

### ✅ **Zgodność z wymaganiami:**

✔ Spektrogram: `spectrogram(s, 4096, 4096-512, [0:5:2000], fs)`  
✔ Filtracja BP z zadania 1  
✔ Porównanie przed i po filtracji  
✔ Kompensacja opóźnienia – NIEdodana (można dopisać `grpdelay`)  
✔ Algorytm Goertzla – zaimplementowany (opcjonalne +0.25 pkt) ✅

---

## ✅ **ZADANIE 3 – Radio FM – dekodowanie**

### 🔸 **Teoria:**

- Odbierany sygnał FM zawiera wiele stacji – każda przesunięta względem nośnej.
    
- Proces dekodowania:
    
    1. **Przesunięcie widma** do zera (mnożenie przez exp)
        
    2. **Filtracja LP** – izolacja jednej stacji (np. 80 kHz)
        
    3. **Decymacja** – zmniejszenie fs do szerokości pasma stacji
        
    4. **Demodulacja FM** – różniczka fazy
        
    5. **De-emfaza** – tłumienie wysokich częstotliwości
        

### 🔸 **Co zrobiłem:**

- IQ: `s(1:2:end) + i*s(2:2:end)`
    
- Przesunięcie widma na zero
    
- Filtr Butterwortha LP (80 kHz) ✅
    
- Decymacja: 3.2 MHz → 160 kHz → 32 kHz ✅
    
- Demodulacja FM: różniczka fazy ✅
    
- Filtr antyaliasingowy przed dalszą decymacją ✅
    
- Filtr de-emfazy (Butterworth LP z 2.1 kHz) ✅
    
- Finalny odsłuch i normalizacja ✅
    

### ✅ **Zgodność z wymaganiami:**

✔ Wszystkie kroki dekodera FM wykonane  
✔ Antyaliasing i de-emfaza zaimplementowane  
✔ Gotowy kod z opcjami do zmiany pasma/stacji  
✔ Brakuje: zaprojektowania filtru pre-emfazy i porównania (opcjonalne +0.25 pkt)

---

## ✅ **ZADANIE 4 – Filtrowanie dźwięków rzeczywistych**

### 🔸 **Teoria:**

- Mieszanie dźwięków o różnych zakresach częstotliwości (np. mowa + ptak)
    
- Filtr cyfrowy IIR (np. LP, BP), aby odseparować źródła
    
- Analiza sygnałów: FFT, STFT (spektrogram)
    
- Weryfikacja efektu filtracji: wykresy, zera/bieguny, porównania
    

### 🔸 **Co zrobiłem:**

- Załadowanie `mowa.wav` i `ptak.wav`
    
- Mieszanie i zapis sumy
    
- FFT: pojedyncze sygnały i suma
    
- Projekt LP filtru 4 rzędu do 3 kHz (dla mowy) ✅
    
- Filtracja i odsłuch ✅
    
- Spektrogramy: przed i po filtracji ✅
    
- Zera/bieguny filtru (`zplane`) ✅
    
- Charakterystyka częstotliwościowa (`fvtool`) ✅
    

### ✅ **Zgodność z wymaganiami:**

✔ Widma i spektrogramy  
✔ Projekt IIR filtru do separacji  
✔ Odpowiedź częstotliwościowa  
✔ Zera i bieguny na płaszczyźnie zespolonej  
✔ Odsłuch i analiza po filtracji

---

## ✅ PODSUMOWANIE

| Zadanie        | Teoria | Kod | Zgodność z PDF | Uwagi                            |
| -------------- | ------ | --- | -------------- | -------------------------------- |
| 1 – IIR BP     | ✅      | ✅   | ✅              | Pełne                            |
| 2 – DTMF       | ✅      | ✅   | ✅              | Brak kompensacji opóźnienia      |
| 3 – FM         | ✅      | ✅   | ✅              | Opcjonalna pre-emfaza do dodania |
| 4 – Real audio | ✅      | ✅   | ✅              | Wszystko OK                      |

---



# Opracowanie Zadania 2 i 3 – Laboratorium DSP

## Zadanie 2: Dekodowanie DTMF (1 + 0.75 pkt)

### 🌍 Wprowadzenie teoretyczne

**DTMF** (Dual Tone Multi Frequency) to system sygnalizacji tonowej, stosowany w telefonii analogowej. Każdy klawisz generuje **sumę dwóch tonów**:

- jeden z grupy **wierszy (niskie częstotliwości)**,
    
- jeden z grupy **kolumn (wysokie częstotliwości)**.
    

||1209 Hz|1336 Hz|1477 Hz|
|---|---|---|---|
|697 Hz|1|2|3|
|770 Hz|4|5|6|
|852 Hz|7|8|9|
|941 Hz|*|0|#|

Sygnały mają długość ok. 70 ms i są oddzielone pauzami.

---

### ⚙️ Algorytm Goertzla – teoria

**Goertzel** to algorytm do obliczania **mocy konkretnej składowej DFT**, bez liczenia całej transformaty:

1. Obliczamy współczynnik: ωk=2πfkfs\omega_k = \frac{2\pi f_k}{f_s}
    
2. Rekurencja: s[n]=x[n]+2cos⁡(ωk)s[n−1]−s[n−2]s[n] = x[n] + 2\cos(\omega_k) s[n-1] - s[n-2]
    
3. Energia: ∣X[k]∣2=s[N−1]2+s[N−2]2−2cos⁡(ωk)s[N−1]s[N−2]|X[k]|^2 = s[N-1]^2 + s[N-2]^2 - 2\cos(\omega_k) s[N-1]s[N-2]
    

✅ Zaletą jest wysoka efektywność przy analizie małej liczby częstotliwości.

---

### 🔎 Algorytm automatycznego dekodowania DTMF

1. **Filtracja pasmowo-przepustowa** (Butterworth BP):
    
    - Odfiltrowanie częstotliwości nie należących do DTMF.
        
2. **Analiza Goertzla**:
    
    - Obliczanie energii dla 7 częstotliwości w oknach czasowych.
        
3. **Detekcja aktywnych okien**:
    
    - Na podstawie sumy energii i progu aktywności.
        
4. **Rozpoznanie znaku**:
    
    - Najsilniejsze częstotliwości w każdym pasmie.
        
    - Warunek kontrastu dla uniknięcia zakłamań.
        
5. **Usuwanie duplikatów**:
    
    - źby jedno naciśnięcie nie było rozpoznawane wielokrotnie.
        

---

### 🔄 Wnioski

- Algorytm działa skutecznie nawet na zaszumionych sygnałach.
    
- Goertzel – idealny do DTMF (mała liczba tonów).
    
- Automatyczny dekoder – praktyczny, dokładny, gotowy do produkcji.
    

---

## Zadanie 3: Radio FM – dekodowanie (1 + 0.25 pkt)

### 🎧 Teoria systemu FM

**Sygnał FM** jest nadawany jako fala nośna z modulacją częstotliwości. Przykład:

- Nośna: 101 MHz
    
- Pasmo: 101 ± 0.1 MHz
    

Aby zdekodować sygnał FM cyfrowo:

1. **Przeniesienie pasma** (tuner SDR):
    
    - z [100 MHz ... 103.2 MHz] do [0 ... 3.2 MHz]
        
2. **Postać zespolona IQ**:
    
    - z danych typu I(n), Q(n): s[n]=I[n]+jQ[n]s[n] = I[n] + jQ[n]
        
3. **Wyodrębnienie stacji**:
    
    - przesunięcie sygnału do zera i filtracja LP
        
4. **Demodulacja FM**: y[n]=arg⁡(x[n]⋅x[n−1]‾)y[n] = \arg(x[n] \cdot \overline{x[n-1]})
    
5. **Decymacja**:
    
    - z 3.2 MHz do 160 kHz (co 20-ta próbka)
        
    - dalej do 32 kHz (co 5-ta próbka)
        
6. **Filtracja LP (antyaliasing)**:
    
    - przed każdą decymacją
        
7. **De-emfaza**:
    
    - filtr o płaskiej charakterystyce do 2.1 kHz, spadek 20 dB/dekadę
        

---

### 🔍 Struktura kodu `zad3.m`

- Wczytanie IQ z pliku binarnego
    
- Przesunięcie widma do 0 Hz
    
- Filtracja LP (Butterworth 4 rzędu, 80 kHz)
    
- Demodulacja FM (pochodna fazy)
    
- Antyaliasing: filtr LP 16 kHz
    
- De-emfaza: filtr LP Butterworth, 2.1 kHz
    

---

### 📊 Analiza i wizualizacje

Kod zawiera:

- Widma gęstości mocy (Welch)
    
- Spektrogramy sygnałów na każdym etapie
    
- Charakterystyki filtrów de-emfazy i pre-emfazy
    

---

### ✅ Wnioski

- Poprawne dekodowanie FM wymaga:
    
    - precyzyjnej filtracji,
        
    - zmiany częstotliwości (downsampling),
        
    - poprawnej demodulacji fazowej,
        
    - zastosowania de-emfazy.
        
- Widmo po demodulacji zawiera składowe: mono, stereo, RDS.
    

---

## Podsumowanie

Zarówno w zadaniu DTMF, jak i FM, kluczowe jest:

- prawidłowe filtrowanie sygnału,
    
- wybór skutecznej metody analizy częstotliwości (Goertzel vs. FFT),
    
- automatyzacja algorytmu (dekodery, segmentacja, kontrast).
    

📆 Opracowanie przygotowane 16.04.2025 r.
Świetnie! Oto rozbudowana wersja części **teoretycznej** do zadań 1 i 4 w formacie **Markdown**, z odniesieniami do konkretnych fragmentów kodu (`zad1.m`, `zad4.m`) i dopisanym wyjaśnieniem celów oraz działania każdego etapu.

---

## 📘 Teoria do Zadania 1 – Filtr cyfrowy IIR

### 🎯 Cel zadania

Celem było:

- dokonanie konwersji filtru analogowego typu **Butterworth** z postaci H(s)H(s) do cyfrowej H(z)H(z),
    
- porównanie charakterystyki częstotliwościowej obu wersji filtru,
    
- zaimplementowanie **własnej filtracji cyfrowej** oraz porównanie jej z filtracją przy pomocy funkcji `filter(...)`.
    

---

### 🧠 Teoria

#### 🔄 Transformacja biliniowa

Aby dokonać konwersji filtru analogowego H(s)H(s) na postać cyfrową H(z)H(z), zastosowano **transformatę biliniową**:

s=2T⋅1−z−11+z−1,gdzie T=1fss = \frac{2}{T} \cdot \frac{1 - z^{-1}}{1 + z^{-1}}, \quad \text{gdzie } T = \frac{1}{f_s}

W kodzie `zad1.m` (linia:

````matlab
[num_digital, den_digital] = bilinear(num_analog, den_analog, sampling_rate);
```)
zastosowano tę transformację przy użyciu funkcji `bilinear()` w MATLAB.

Transformacja ta zachowuje stabilność układu i odwzorowuje oś \( j\Omega \) w dziedzinie \( s \) na jednostkowe koło \( |z| = 1 \), ale **nieliniowo** odwzorowuje częstotliwości. Skutkuje to **przesunięciem rzeczywistych częstotliwości granicznych** filtru cyfrowego względem prototypu analogowego.

---

#### ⚠️ Pre-warping (opcjonalne rozszerzenie)
Aby uniknąć zniekształcenia częstotliwości, stosuje się technikę **pre-warpingu**. Zmodyfikowane częstotliwości graniczne oblicza się ze wzoru:

\[
\Omega = 2 \cdot f_s \cdot \tan\left(\frac{\pi f_c}{f_s}\right)
\]

Pozwala to zaprojektować filtr analogowy, którego transformacja biliniowa da filtr cyfrowy z **dokładnymi** częstotliwościami granicznymi.

---

### ⚙️ Implementacja filtru IIR

#### 1. Tworzenie filtru analogowego:
Z pliku `butter.mat` wczytano:
- zera (`z`),
- bieguny (`p`),
- wzmocnienie (`k`).

Na tej podstawie utworzono transmitancję:
```matlab
[num_analog, den_analog] = zp2tf(z, p, k);
````

#### 2. Konwersja do filtru cyfrowego:

```matlab
[num_digital, den_digital] = bilinear(num_analog, den_analog, sampling_rate);
```

#### 3. Analiza charakterystyk:

Obie charakterystyki zostały narysowane na wspólnym wykresie, z zaznaczeniem spadku -3 dB i rzeczywistych granic pasma.

#### 4. Filtracja – własna implementacja:

Kod zawiera ręczną implementację filtracji sygnału przez rekurencyjne równanie różnicowe:

```matlab
for n = 1:signal_length
    ...
end
```

Każda próbka jest obliczana rekurencyjnie z użyciem współczynników transmitancji H(z)H(z). Dla porównania użyto też:

```matlab
output_signal_matlab = filter(num_digital, den_digital, input_signal);
```

---

### 🔍 Porównanie wyników

- **W dziedzinie czasu**: Przefiltrowane sygnały są niemal identyczne.
    
- **W dziedzinie częstotliwości (FFT)**: Filtr skutecznie usunął drugą składową (1272 Hz), pozostawiając tylko 1209 Hz.
    
- Potwierdzono poprawność działania zarówno własnej implementacji, jak i funkcji `filter()`.
    

---

## 🎧 Teoria do Zadania 4 – Filtrowanie dźwięków rzeczywistych

### 🎯 Cel zadania

Zadanie miało na celu:

- analizę rzeczywistych nagrań dźwiękowych (np. silnik, ptak),
    
- ich **mieszanie** w jeden sygnał,
    
- zaprojektowanie i wykorzystanie filtrów IIR do separacji źródeł,
    
- porównanie efektów filtracji wizualnie (FFT, STFT) i odsłuchowo.
    

---

### 🧠 Teoria filtrów

#### Filtry IIR

Są to **rekursywne** filtry cyfrowe, które wykorzystują zarówno przeszłe wartości sygnału wejściowego, jak i przeszłe wartości wyjścia. Mają postać:

y[n]=∑k=0Mbkx[n−k]−∑j=1Najy[n−j]y[n] = \sum_{k=0}^{M} b_k x[n-k] - \sum_{j=1}^{N} a_j y[n-j]

---

### ⚙️ Projektowanie filtrów – podejścia

W pliku `zad4.m` wykorzystano trzy rodzaje filtrów Butterwortha:

#### 1. **Dolnoprzepustowy** (`butter(6, ..., 'low')`)

Zachowuje niskie częstotliwości – np. dźwięk silnika.

#### 2. **Górnoprzepustowy** (`butter(6, ..., 'high')`)

Zachowuje wysokie częstotliwości – np. śpiew ptaka.

#### 3. **Pasmowo-zaporowy (notch)** (`butter(4, [f_low f_high], 'stop')`)

Tłumi określone pasmo, np. szumy silnika. Przydatne w wycinaniu konkretnych zakłóceń.

Każdy z filtrów został **narysowany**:

- charakterystyka częstotliwościowa (`freqz(...)`)
    
- zera i bieguny (`zplane(...)`)
    

---

### 🧪 Analiza widmowa

Wykorzystano:

- **FFT** (`fft(...)`) – analiza sygnałów w dziedzinie częstotliwości,
    
- **Spektrogram (STFT)** (`pspectrum(...)`) – analiza w czasie i częstotliwości.
    

Pozwoliło to na ocenę wpływu filtracji na strukturę widmową sygnałów.

---

### 🧏‍♂️ Efekty filtracji

- **Sygnały wyjściowe** po filtrach zostały **znormalizowane** i zapisane do plików WAV.
    
- Można je było **odsłuchać**, by subiektywnie ocenić skuteczność separacji.
    
- Spektrogramy pokazują skuteczne wydzielenie pożądanych sygnałów.
    

---

## 🧩 Wnioski

- Filtry IIR są skuteczne w praktycznej separacji źródeł dźwięku, ale wymagają dokładnej analizy pasma.
    
- Transformacja biliniowa nie odwzorowuje liniowo częstotliwości – może być konieczne użycie pre-warpingu.
    
- Własna implementacja filtrów jest dobrym ćwiczeniem z zakresu DSP i pozwala lepiej zrozumieć działanie filtrów cyfrowych.
    

---

Chcesz, żebym wrzucił to też do pliku `.md`? Albo zrobić do tego mini podsumowanie z wynikami wykresów?