
# **Analiza Teorii i Kodów – Laboratorium 3**

---

## **Zadanie 1: DFT sygnału harmonicznego (`Zad1v3.m`)**
### **Teoria**  
- **Cel:** Obliczenie DFT sygnału złożonego z dwóch kosinusoid (100 Hz i 200 Hz) przy użyciu macierzy transformacji DFT.  
- **Kluczowe pojęcia:**  
  - **DFT jako macierz:** Transformacja jest iloczynem macierzy `A` i sygnału `x`. 
  - **Widmo:** Składa się z części rzeczywistej (kosinusy), urojonej (sinusy), modułu (amplituda) i fazy.  
  - **Aliasing:** Zmiana `f1=100 Hz` na `125 Hz` powoduje, że częstotliwość nie pasuje do siatki DFT (Δf=10 Hz dla `N=100`), co skutkuje **rozmyciem energii** między sąsiednie bin-y.  

### **Kod**  
1. **Generacja sygnału:**  
   ```matlab
   x = A1*cos(2*pi*f1*t + phi1) + A2*cos(2*pi*f2*t + phi2);
   ```  
   - `t` to wektor czasu o długości `N=100` próbek.  
2. **Macierz DFT `A`:**  
   ```matlab
   for k = 0:N-1
       for n = 0:N-1
           A(k+1, n+1) = (1/sqrt(N)) * exp(-1i*2*pi*k*n/N);
       end
   end
   ```  
   - Każdy wiersz odpowiada innej częstotliwości.  
3. **Rekonstrukcja:**  
   ```matlab
   B = A'; % Macierz odwrotna (sprzężenie i transpozycja)
   x_recon = real(B * X); % Ignorowanie części urojonej (błędy numeryczne)
   ```  
4. **Zmiana `f1=125 Hz`:**  
   - DFT nie rozróżnia 125 Hz od 125 ± k·fs (np. 125 Hz vs 1125 Hz).  

---

## **Zadanie 2: Porównanie DFT, zero-padding i DtFT (`Zad2v2.m`)**  
### **Teoria**  
- **DFT bez zer (`X1`):** Próbki widma co `fs/N = 10 Hz` (dla `N=100`).  
- **Zero-padding (`X2`):** Dodanie `M=100` zer zwiększa liczbę punktów DFT, ale **nie poprawia rozdzielczości** (Δf nadal 10 Hz).  
- **DtFT (`X3`):** Ciągłe widmo obliczane analitycznie. Pokazuje idealne kształty, ale jest obliczeniowo kosztowne.  

### **Kod**  
1. **Dopełnienie zerami:**  
   ```matlab
   xz = [x zeros(1, M)]; % Sygnał x + M zer (długość N+M=200)
   ```  
2. **Wektory częstotliwości:**  
   - `fx1 = fs*(0:N-1)/N` → 0, 10, 20, ..., 990 Hz.  
   - `fx2 = fs*(0:(N+M)-1)/(N+M)` → 0, 5, 10, ..., 995 Hz (interpolacja).  
3. **DtFT dla pełnego zakresu:**  
   ```matlab
   f_full = -2000:0.25:2000; % Pokazuje okresowość widma (co fs=1000 Hz).
   ```  
   - Widmo DFT jest okresowe, ale standardowo rysuje się tylko do `fs/2=500 Hz`.

---

## **Zadanie 3: Wpływ okien czasowych (`Zad3v2.m`)**  
### **Teoria**  
- **Okna czasowe:** Redukują przecieki widmowe poprzez "wyciszanie" brzegów sygnału.  
- **Parametry okien:**  
  - **Prostokątne:** Najgorsze tłumienie listków bocznych, ale najlepsza rozdzielczość.  
  - **Czebyszewa:** Kontrolowane tłumienie listków bocznych (im wyższe tłumienie, tym lepiej).  

### **Kod**  
1. **Definicja DtFT:**  
   ```matlab
   compute_dtft = @(x, N, f, fs) (x * exp(-1j * 2 * pi * (0:N-1)' * f / fs)).';
   ```  
   - Oblicza DtFT dla dowolnego wektora `f`.  
2. **Mnożenie przez okna:**  
   ```matlab
   x1 .* w_rect % Sygnał x1 przemnożony przez okno prostokątne
   ```  
   - Okno Hamminga: `w_hamming = hamming(N1)'`.  
3. **Wyniki dla `N=1000`:**  
   - Większe `N` → węższe listki główne (lepsza rozdzielczość).  

---

## **Zadanie 4: Analiza sygnału ADSL (`Zad4v2.m`)**  
### **Teoria**  
- **Ramki ADSL:** Każda ramka ma `N=512` próbek i prefiks `M=32`.  
- **DFT ramki:** Identyfikacja aktywnych podnośnych (harmonicznych) w widmie.  

### **Kod**  
1. **Indeksowanie ramek:**  
   ```matlab
   start_idx = m*(N + M) + M + 1; % Pominięcie prefiksu (M+1 próbek)
   ```  
2. **Dynamiczny próg:**  
   ```matlab
   threshold = max(mean(frame_fft_mag) * 2, 10); % Unika wykrywania szumu
   ```  
   - `findpeaks` wykrywa piki powyżej progu.  
3. **Wyniki:**  
   ```matlab
   disp(['Ramka ', num2str(m+1), ': Aktywne harmoniczne: ', idx_str]);
   ```  
   - Przykład: `Ramka 1: Aktywne harmoniczne: 5, 10, 15`.  

---

## **Zadanie 5: Analiza EKG (`Zad5.m`)**  
### **Teoria**  
- **Tętno:** Obliczane z odstępów RR (czas między załamkami R).  
- **Widmo DFT:** Pokazuje składowe niskoczęstotliwościowe (np. ruch mięśni) i częstotliwość tętna.  

### **Kod**  
1. **Detekcja załamków R:**  
   ```matlab
   [pks, locs] = findpeaks(ecg, 'MinPeakHeight', 0.7*max(ecg));
   ```  
   - `locs` to indeksy załamków R.  
2. **Widmo decybelowe:**  
   ```matlab
   20*log10(X_amp) % Przeliczenie amplitudy na decybele
   ```  
   - Skala logarytmiczna lepiej pokazuje słabe składowe.  

---

## **Zadanie 6: Filtracja w dziedzinie DFT (`Zad6.m`)**  
### **Teoria**  
- **Filtracja DFT:** Usunięcie składowych częstotliwościowych poprzez wyzerowanie odpowiednich binów.  
- **Symetria widma:** Aby sygnał po IDFT był rzeczywisty, należy usunąć zarówno częstotliwości dodatnie, jak i ujemne.  

### **Kod**  
1. **Wyzerowanie niskich częstotliwości:**  
   ```matlab
   X_sum_filt(1:k_low) = 0; % Częstotliwości dodatnie
   X_sum_filt(end - k_low + 1:end) = 0; % Odbicia lustrzane (ujemne)
   ```  
2. **Odsłuch:**  
   ```matlab
   sound(sygnal_filtrowany, fs); % Słyszalny głównie ptak
   ```  
   - Jeśli występują składowe urojone, MATLAB wyświetli ostrzeżenie.  

---

# **Podsumowanie**  
- **DFT vs DtFT:** DFT to próbki DtFT; DtFT jest ciągły, ale obliczeniowo droższy.  
- **Okna:** Wybór okna zależy od kompromisu między rozdzielczością a tłumieniem przecieków.  
- **Zero-padding:** Poprawia wizualizację, ale nie rozdzielczość.  
- **Filtracja DFT:** Wymaga symetrycznego usuwania częstotliwości, aby uniknąć składowych urojonych.  
___

# **Kompendium: Analiza częstotliwościowa (DFT, DtFT, okna, zero-padding)**

---

## **1. DFT vs DtFT: Podstawowe różnice**
| **Parametr**         | **DFT (Discrete Fourier Transform)**                          | **DtFT (Discrete-Time Fourier Transform)**                     |
|----------------------|---------------------------------------------------------------|----------------------------------------------------------------|
| **Definicja**         | Dyskretne próbkowanie DtFT dla skończonego sygnału.           | Ciągłe widmo dla sygnału o dowolnej długości (teoretycznie nieskończonej). |
| **Wektor częstotliwości** | Dyskrety: `f_k = k * fs/N` (k=0,1,...,N-1)                  | Ciągły: `f ∈ [0, fs)` lub dowolny zakres (np. `-fs/2` do `fs/2`). |
| **Zastosowanie**      | Szybkie obliczenia (FFT), analiza sygnałów rzeczywistych.      | Teoretyczna analiza, dokładne modelowanie widma.              |
| **Skalowanie**        | Amplitudy skalowane przez `1/N` (lub `1/sqrt(N)` w zależności od konwencji). | Brak skalowania lub zależne od implementacji.                |
| **Przykład w kodzie** | `X = fft(x)/N`                                               | `X3 = (x * exp(-1j*2*pi*n*f/fs)).' / N`                      |

---

## **2. Okna czasowe: Dlaczego i jak działają?**
### **Cel stosowania okien**  
Redukcja **przecieków widmowych** (ang. *spectral leakage*), czyli rozmycia energii sygnału do sąsiednich częstotliwości, gdy sygnał nie jest idealnie periodyczny w oknie obserwacji.

### **Parametry okien**
- **Listek główny** (main lobe): Określa **rozdzielczość** – im węższy, tym lepiej rozróżniamy bliskie częstotliwości.  
- **Listki boczne** (side lobes): Określają **tłumienie przecieków** – im niższe, tym mniej zakłóceń.  

| **Okno**        | Listek główny | Listki boczne | Zastosowanie                        |     |
| --------------- | ------------- | ------------- | ----------------------------------- | --- |
| **Prostokątne** | Wąski         | Wysokie       | Sygnały periodyczne, szybka analiza |     |
| **Hamminga**    | Średni        | Niskie        | Uniwersalne                         |     |
| **Blackmana**   | Szeroki       | Bardzo niskie | Redukcja przecieków                 |     |
| **Czebyszewa**  | Dostosowany   | Kontrolowane  | Aplikacje wymagające precyzji       |     |

### **Przykład z kodu (`Zad3v2.m`)**  
```matlab
w_rect = rectwin(N1)'; % Okno prostokątne
X_rect = compute_dtft(x1 .* w_rect, N1, f, fs); % Mnożenie sygnału przez okno
```
- **Efekt:** Sygnał z oknem Hamminga ma mniejsze przecieki, ale szerszy listek główny niż prostokątne.

---

## **3. Długość sygnału (N) i jej wpływ**
### **Rozdzielczość częstotliwościowa**  
- **Im większe N**, tym mniejsze \(\Delta f\) → lepsze rozróżnienie bliskich częstotliwości.  
- **Przykład:**  
  - Dla \(N=100\), \(f_s=1000\) Hz: \(\Delta f = 10\) Hz.  
  - Dla \(N=1000\): \(\Delta f = 1\) Hz → wykryjesz różnicę 1 Hz między składowymi.

### **Zmiana N w kodzie (`Zad3v2.m`)**  
- Dla `N=1000` (vs `N=100`):  
  ```matlab
  n2 = (0:N2-1); % N2=1000
  x2 = A1 * cos(2*pi*f1*t2 + phi1) + A2 * cos(2*pi*f2*t2 + phi2);
  ```  
  - **Efekt:** Węższe listki główne w widmie → lepsza rozdzielczość.

---

## **4. Zero-padding: Po co dodajemy zera?**
### **Definicja**  
Dopełnienie sygnału \(M\) zerami do długości \(N+M\).  
```matlab
xz = [x zeros(1, M)]; % Przykład z Zad2v2.m
```  

### **Cele**  
- **Interpolacja widma DFT:** Więcej punktów → płynniejszy wykres.  
- **Nie poprawia rozdzielczości!** Prawdziwa rozdzielczość zależy od oryginalnego \(N\).  

### **Przykład**  
- Sygnał \(N=100\), \(M=100\) → \(N+M=200\).  
- DFT ma 200 punktów, ale \(\Delta f = \frac{1000}{100} = 10\) Hz (nie 5 Hz!).  

### **Wizualizacja**  
- **Bez zer:** DFT to dyskretne punkty (np. co 10 Hz).  
- **Z zerami:** DFT interpolowane (np. co 5 Hz), ale nowe punkty nie niosą nowej informacji.  

---

## **5. Podsumowanie wpływu parametrów**
| **Parametr**         | **Efekt**                                  | **Kompromis**                             |  
|----------------------|--------------------------------------------|-------------------------------------------|  
| **Okno**             | Mniejsze przecieki, ale szerszy listek główny | Redukcja szumów vs utrata rozdzielczości |  
| **Zwiększenie N**    | Lepsza rozdzielczość (\(\Delta f \downarrow\)) | Większe zużycie pamięci i czasu obliczeń |  
| **Zero-padding**     | Gładsze widmo (lepsza wizualizacja)        | Brak poprawy rozdzielczości              |  

---

## **6. Przykłady zadań i zmiany parametrów**
### **Zadanie 1 (`Zad1v3.m`)**  
- **Zmiana \(f1=100 \to 125\) Hz:**  
  - Dla \(N=100\), \(\Delta f = 10\) Hz → 125 Hz **nie pasuje** do siatki DFT (125/10=12.5 → energia rozleje się na sąsiednie bin-y).  
  - **Efekt:** Rozmyte piki w widmie (aliasing w dziedzinie częstotliwości).

### **Zadanie 2 (`Zad2v2.m`)**  
- **DtFT vs DFT:**  
  - DtFT jest ciągły, DFT to jego próbki.  
  - DtFT dla `f=-2000:0.25:2000` pokazuje **okresowość widma** (co \(f_s = 1000\) Hz).  

### **Zadanie 3 (`Zad3v2.m`)**  
- **Czebyszew vs Blackman:**  
  - Okno Czebyszewa z tłumieniem 120 dB ma niższe listki boczne niż 100 dB, ale szerszy listek główny.  

---

## **7. Kluczowe wnioski**  
1. **DFT to dyskretna wersja DtFT** – próbkuje widmo w równych odstępach.  
2. **Okna** są niezbędne do redukcji przecieków, ale zawsze jest kompromis między rozdzielczością a tłumieniem.  
3. **Zero-padding** to trik wizualny – nie dodaje informacji o sygnale.  
4. **Prawdziwa rozdzielczość** zależy tylko od czasu obserwacji sygnału (\(T = N/f_s\)).