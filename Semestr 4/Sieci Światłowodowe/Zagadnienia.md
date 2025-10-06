Rozchodzenie się sygnału optycznego w światłowodzie

Natura światła może być opisana przy użyciu modelu cząsteczkowego (fotony, efekt fotoelektryczny) lub modelu falowego (równania Maxwella, interferencje). Podstawowe właściwości światłowodu można omówić, stosując podejście optyki geometrycznej. Podejście optyki geometrycznej można zastosować tylko przy założeniu, że promień rdzenia światłowodu jest znacznie większy niż długość fali nośnika optycznego. Zjawisko całkowitego wewnętrznego odbicia jest kluczowe dla prowadzenia światła w światłowodzie.

### Światłowody wielomodowe i jednomodowe

- **Światłowody wielomodowe (MMF)**: W światłowodach wielomodowych sygnał optyczny propaguje w postaci wielu modów. Każdy mod charakteryzuje się inną stałą propagacji β, która odzwierciedla prędkość propagacji impulsu energii danego modu. Mody w światłowodzie wielomodowym są rozwiązaniami równań Maxwella spełniającymi warunki brzegowe na granicy rdzeń-płaszcz, parametryzowanymi przez funkcje Bessela. Liczba modów prowadzonych w MMF GI (ze skokowym profilem współczynnika załamania) jest mniejsza niż w MMF SI (ze skokowym profilem).
- **Światłowody jednomodowe (SMF)**: Światłowody jednomodowe zostały zaprojektowane, aby przezwyciężyć problem zniekształceń sygnału spowodowanych propagacją wielu modów. Światłowód jednomodowy prowadzi tylko jeden, fundamentalny mod LP01. Aby to osiągnąć, światłowód musi spełniać warunek odcięcia (cut-off condition), gdzie wartość znormalizowanej liczby falowej V musi być mniejsza niż 2,405. W światłowodzie jednomodowym sygnał propaguje częściowo w rdzeniu i częściowo w płaszczu. Z tego powodu SMF charakteryzuje się **polem modowym (MFD)** zamiast promieniem rdzenia.

### Światłowody o skokowym i gradientowym profilu (Step Index, Graded Index)

- **Step Index (SI)**: Posiada stały współczynnik załamania światła w rdzeniu i niższy, stały współczynnik w płaszczu.
- **Graded Index (GI)**: Współczynnik załamania światła w rdzeniu zmienia się stopniowo wraz z odległością od centrum, malejąc w kierunku płaszcza. Profil współczynnika załamania dla MMF GI można opisać wzorem. Liczba modów w MMF GI jest mniejsza niż w MMF SI.

### Dyspersja międzymodowa (intermodal dispersion)

Jest to zjawisko, w którym różne mody sygnału optycznego propagują z różnymi prędkościami w światłowodzie. Różne prędkości prowadzą do poszerzenia impulsów i nakładania się sąsiednich impulsów, co jest powszechnie określane jako **interferencja międzysymbolowa (ISI)**. Dyspersja międzymodowa (lub modalna) jest problemem w światłowodach wielomodowych. Jakościowe oszacowanie dyspersji międzymodowej w MMF SI można przeprowadzić analizując ścieżki promieni (modów) o różnym kącie propagacji. Różnica w czasach propagacji dla modów jest źródłem dyspersji międzymodowej.

### Dyspersja materiałowa i falowodowa (Chromatic Dispersion - CD)

Dyspersja (ogólnie) to zjawisko, w którym różne komponenty sygnału optycznego propagują z różnymi prędkościami. W światłowodach jednomodowych (SMF) występują głównie dyspersja chromatyczna i dyspersja polaryzacyjna.

- **Dyspersja chromatyczna (CD)** składa się z dyspersji materiałowej i dyspersji falowodowej. Dla standardowych światłowodów telekomunikacyjnych głównym składnikiem CD jest dyspersja materiałowa.
- **Dyspersja materiałowa** wynika z częstotliwościowej zależności współczynnika załamania światła materiału rdzenia (np. krzemionki SiO2). Różne "komponenty widmowe" (różne długości fal w widmie sygnału) mają różne współczynniki załamania, co prowadzi do różnych prędkości propagacji. Poszerzenie impulsu spowodowane dyspersją materiałową zależy od szerokości widmowej sygnału Δλ i pochodnej współczynnika załamania względem długości fali.
- **Dyspersja falowodowa** wynika z faktu, że różne "komponenty przestrzenne" (mody w MMF lub rozkład pola modowego w SMF) widzą różne efektywne współczynniki załamania. W światłowodach jednomodowych sygnał propaguje częściowo w rdzeniu i częściowo w płaszczu, które mają różne współczynniki załamania. Ta różnica współczynników jest źródłem dyspersji falowodowej. Dyspersję falowodową można wykorzystać do kompensacji dyspersji materiałowej, co jest stosowane w światłowodach o spłaszczonej dyspersji (flattened dispersion fibres) lub światłowodach o przesuniętej dyspersji (dispersion shifted fibres). Wartość współczynnika dyspersji chromatycznej (Dch​) jest kluczowym parametrem SMF, podawanym w jednostkach ps/nm·km.

### Budżet mocy optycznej (Optical Link Budget)

Budżet mocy to oszacowanie strat sygnału w łączu optycznym i porównanie ich z dostępną mocą nadajnika i czułością odbiornika. Przykład budżetu mocy dla systemu 10 Gbit/s na 80 km pokazuje, że sumaryczna strata (16,0 dB tłumienia włókna + 1,2 dB strat na złączach + 1,5 dB strat na spawach + 2,0 dB kary za dyspersję chromatyczną) wynosi 20,7 dB. Przy nadajniku 10 dBm i odbiorniku -10 dBm dostępny budżet mocy to 20 dB, co jest niewystarczające. Sugerowane rozwiązania to lepszy odbiornik (np. -11 dBm) lub zmniejszenie kary za dyspersję. Kara za dyspersję (CD power penalty) jest dodatkową stratą mocy, którą należy uwzględnić w budżecie mocy ze względu na poszerzenie impulsu spowodowane dyspersją. Typowo kara ta wynosi 1-2 dB.

### Water peak

Jest to zwiększone tłumienie sygnału w światłowodach krzemionkowych, występujące w okolicy 1383 nm, spowodowane absorpcją przez pozostałości wody (grupy OH) w szkle. Nowsze światłowody SMF typu G.652C i G.652D mają zredukowane tłumienie w paśmie 1383 ± 3 nm (maksymalnie 0,4 dB/km), co pozwala na rozszerzenie użytecznego okna transmisyjnego do całego zakresu 1260 – 1625 nm.

### Typy światłowodów: OM-1/2/3/4/5 i G.652, G.655, G.657

- **Światłowody wielomodowe (MMF)** są klasyfikowane według normy ISO/IEC 11801 (oraz ITU-T G.651):
    - **G.651**: Charakteryzuje światłowód wielomodowy o profilu gradientowym 50/125 µm.
    - **OM-1**: Określa minimalną przepustowość OFL (Overfilled Launch) na 200 MHz·km przy 850 nm i 500 MHz·km przy 1300 nm. Zazwyczaj 62.5/125 µm.
    - **OM-2**: Określa minimalną przepustowość OFL na 500 MHz·km przy 850 nm i 500 MHz·km przy 1300 nm. Zazwyczaj 50/125 µm.
    - **OM-3**: Określa minimalną przepustowość OFL na 1500 MHz·km przy 850 nm i 500 MHz·km przy 1300 nm. Światłowód zoptymalizowany dla laserów VCSEL 850 nm.
    - **OM-4**: Określa minimalną przepustowość OFL na 3500 MHz·km przy 850 nm i 500 MHz·km przy 1300 nm. Światłowód o wyższej przepustowości niż OM-3 przy 850 nm.
    - **OM-5**: Określa minimalną przepustowość OFL jak dla OM4, światłowód do SWDM (850, 880, 910, 940 nm).
- **Światłowody jednomodowe (SMF)** są klasyfikowane według zaleceń ITU-T:
    - **G.652**: Standardowy światłowód jednomodowy. Oryginalnie zoptymalizowany dla 1310 nm, ale może być używany w paśmie 1550 nm. Nowsze wersje (C, D) mają zredukowany water peak przy 1383 nm. Stosowany w sieciach 10GBase-LR/LW i 40GBase-LR4.
    - **G.653**: Światłowód jednomodowy z przesuniętą dyspersją (DSF). Nominalna zerowa dyspersja chromatyczna w paśmie 1550 nm. Ze względu na bardzo małą dyspersję w paśmie C i silne efekty nieliniowe (szczególnie FWM), jest trudny do zastosowania w systemach DWDM.
    - **G.654**: Światłowód jednomodowy z przesuniętym punktem odcięcia (cut-off shifted fibre). Zoptymalizowany dla pracy w paśmie 1500-1600 nm. Charakteryzuje się niskim tłumieniem w trzecim oknie transmisyjnym (np. 0.184 dB/km przy 1550 nm) i większym polem modowym, co pozwala na obsługę wyższych poziomów mocy. Typowa dyspersja chromatyczna to 20-22 ps/nm·km przy 1550 nm. Zaprojektowany głównie do zastosowań podmorskich dalekiego zasięgu.
    - **G.655**: Światłowód jednomodowy o niezerowej przesuniętej dyspersji (NZ-DSF - Non-Zero Dispersion Shifted Fibre). Charakteryzuje się niezerową dyspersją chromatyczną w paśmie 1550 nm (1530-1565 nm). Ta niezerowa dyspersja pomaga ograniczać wzrost efektów nieliniowych (zwłaszcza FWM), które są szkodliwe w systemach DWDM.
    - **G.656**: Światłowód o niezerowej dyspersji dla transportu szerokopasmowego. Charakteryzuje się dodatnią wartością współczynnika dyspersji chromatycznej większą od zera w zakresie 1460-1625 nm. Może być stosowany w systemach CWDM i DWDM. Dyspersja w zakresie 2-14 ps/nm·km.
    - **G.657**: Światłowód jednomodowy niewrażliwy na straty gięciowe (bending-loss insensitive) dla sieci dostępowych. Wersje G.657.A są podzbiorami G.652.D z niższymi stratami gięciowymi (A1 dla min. promienia 10 mm, A2 dla 7.5 mm). Wersje G.657.B nie spełniają standardowej specyfikacji SMF, mają wyższą dyspersję, ale są odporne na bardzo małe promienie gięcia (B2 dla 7.5 mm, B3 dla 5 mm).

### Tłumienie światłowodu (Attenuation)

Tłumienie sygnału w światłowodzie jest spowodowane dwiema grupami efektów: stratami zależnymi od materiału (absorpcja materiałowa, rozpraszanie sygnału) oraz stratami zależnymi od struktury falowodu. Typowe tłumienie sygnału optycznego wynosi 0,2 – 0,3 dB/km.

- **Absorpcja materiałowa**: Wynika z pochłaniania energii przez materiał światłowodu. Przykładowo, water peak przy 1383 nm jest formą absorpcji.
- **Rozpraszanie sygnału**: Dominującym mechanizmem strat jest rozpraszanie Rayleigha (RS). RS powstaje w wyniku fluktuacji gęstości szkła krzemionkowego na poziomie mikroskopowym. Intensywność RS jest odwrotnie proporcjonalna do czwartej potęgi długości fali (αs​∼1/λ4).
- **Straty zależne od falowodu**: obejmują straty na makrogięciach i mikrogięciach. Makrogięcia (np. promień gięcia większy niż 10 cm) zazwyczaj nie powodują znacznego wzrostu tłumienia. Mikrogięcia (nieregularności powierzchni granicznej rdzeń-płaszcz) mogą być źródłem poważnych strat. Całkowite tłumienie w sekcji kabla optycznego (elementary cable section) zależy od długości włókien, ich współczynników tłumienia, średnich strat na spawach i liczby spawów, a także średnich strat na złączach i liczby złącz.

### Dyspersja polaryzacyjna (PMD - Polarisation Mode Dispersion)

Mod fundamentalny w światłowodzie jednomodowym składa się z dwóch ortogonalnie spolaryzowanych modów (zdegenerowanych). PMD jest zjawiskiem stochastycznym. Temperatura, ciśnienie i niedoskonałości światłowodu mają bezpośredni wpływ na współczynnik PMD (DPMD​). Wpływ PMD na propagację sygnału jest mierzony za pomocą **różnicowego opóźnienia grupowego (DGD - Differential Group Delay)**, ΔτPMD​. DPMD​ jest parametrem światłowodu, będącym średnią DGD na jednostkę długości. Typowa wartość DPMD​ mieści się w zakresie 0,1 – 0,5 ps/km$^{1/2}$. Starsze światłowody mogą mieć DPMD​ do 2 ps/km$^{1/2}.DlakroˊtkichsˊwiatłowodoˊwsˊrednieDGDjestproporcjonalnedodługosˊci(\Delta\tau \sim L$), natomiast dla długich jest proporcjonalne do pierwiastka kwadratowego z długości (Δτ∼L![](data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="400em" height="1.08em" viewBox="0 0 400000 1080" preserveAspectRatio="xMinYMin slice"><path d="M95,702
c-2.7,0,-7.17,-2.7,-13.5,-8c-5.8,-5.3,-9.5,-10,-9.5,-14
c0,-2,0.3,-3.3,1,-4c1.3,-2.7,23.83,-20.7,67.5,-54
c44.2,-33.3,65.8,-50.3,66.5,-51c1.3,-1.3,3,-2,5,-2c4.7,0,8.7,3.3,12,10
s173,378,173,378c0.7,0,35.3,-71,104,-213c68.7,-142,137.5,-285,206.5,-429
c69,-144,104.5,-217.7,106.5,-221
l0 -0
c5.3,-9.3,12,-14,20,-14
H400000v40H845.2724
s-225.272,467,-225.272,467s-235,486,-235,486c-2.7,4.7,-9,7,-19,7
c-6,0,-10,-1,-12,-3s-194,-422,-194,-422s-65,47,-65,47z
M834 80h400000v40h-400000z"></path></svg>)​), co jest spowodowane losowym sprzężeniem modów i rotacją osi dwójłomności wzdłuż światłowodu. **Dwójłomność (birefringence)** może być wewnętrzna (błędy w procesie produkcji, dwójłomność geometryczna lub naprężeniowa) lub zewnętrzna (siły zewnętrzne podczas okablowania i instalacji). Aby system działał poprawnie (np. z karą 1dB i dostępnością 1 - 4·10⁻⁵), wartość ΔτPMD​ musi być niższa niż 0,1 · Tbit​ (czas trwania bitu). Wartość DPMD​ linku jest często podawana jako LDV (Link Design Value) lub PMDQ.

### Efekty nieliniowe (SPM, XPM, FWM, SBS, SRS)

Maksymalny poziom mocy sygnału optycznego propagującego w światłowodzie jest ograniczony przez obecność efektów nieliniowych. Efekty nieliniowe zależą od intensywności sygnału optycznego (mocy na jednostkę powierzchni) oraz od długości i powierzchni przekroju poprzecznego światłowodu (efektywna długość, efektywna powierzchnia). Im dłuższy link, tym silniejsze oddziaływanie i gorszy efekt nieliniowości. Zazwyczaj efektywna długość wynosi około 20 km. Duże pole efektywne (Aeff​) oznacza, że światłowód może obsłużyć większą moc optyczną bez podatności na efekty nieliniowe. NZ-DSF (G.655) mają zazwyczaj Aeff​ około 50 µm², podczas gdy "Large effective area fibers" (np. LEAF©) mają Aeff​ ~ 70 µm², a standardowe SMF (G.652) ~ 85 µm².

- **Rozpraszanie (Scattering)**: Interakcja fali świetlnej z drganiami molekularnymi (fononami) ośrodka. Obejmuje:
    - **SBS (Stimulated Brillouin Scattering)**: Rozpraszanie wsteczne. Powoduje przeniesienie znacznej mocy optycznej z sygnału propagującego do przodu na sygnał propagujący do tyłu, gdy próg mocy SBS zostanie przekroczony. Jest to zjawisko wąskopasmowe (przesunięcie częstotliwości około 11 GHz przy 1550 nm). Ma najniższy próg mocy spośród efektów nieliniowych (typ. 5-10 mW dla laserów modulowanych zewnętrznie, 20-30 mW dla modulowanych bezpośrednio). Efektywnie ogranicza moc sygnału. Nie ma wpływu na systemy WDM (poza wpływem na pojedynczy sygnał).
    - **SRS (Stimulated Raman Scattering)**: Rozpraszanie, które powoduje, że fala o krótszej długości (większej energii) działa jako pompa dla fal o dłuższych długościach (mniejszej energii). Energia przenoszona jest z krótszych fal na dłuższe. Jest to efekt szerokopasmowy (do 215 nm). Może być wykorzystany do budowy wzmacniaczy optycznych (rozproszonych). W systemach wielokanałowych (WDM) SRS może pogorszyć stosunek sygnału do szumu dla krótszych fal, ponieważ część ich mocy jest przekazywana do kanałów o dłuższych falach. Ogranicza całkowitą pojemność systemu.
- **Efekt Kerra**: Zmiana współczynnika załamania w zależności od gęstości pola elektromagnetycznego (intensywności sygnału). Obejmuje:
    - **SPM (Self-Phase Modulation)**: Modulacja fazy sygnału przez jego własną intensywność. Zmienność intensywności sygnału w czasie indukuje modulację jego własnej fazy. SPM jest źródłem "ćwierkania" impulsu (pulse chirp). Kara zniekształceń spowodowana SPM rośnie wraz z mocą kanału i prędkością bitową.
    - **XPM (Cross-Phase Modulation)**: W systemach wielokanałowych, zmiany intensywności w jednym kanale wpływają na fazę sygnału w sąsiednich kanałach. Prowadzi do poszerzenia widma sygnału i może powodować poważne przesłuchy międzykanałowe. Wielkość poszerzenia widma zależy od odstępu międzykanałowego i dyspersji chromatycznej (ponieważ dyspersja powoduje rozdzielanie się impulsów). Odstępy międzykanałowe 100 GHz są zazwyczaj wystarczające, aby zredukować efekty XPM.
    - **FWM (Four Wave Mixing)**: Interakcja dwóch lub trzech fal optycznych o różnych długościach fal generuje nowe fale optyczne ("produkty mieszania" lub "pasma boczne") o innych długościach fal. Produkcja FWM jest wysoce efektywna, gdy spełniony jest warunek dopasowania fazowego. FWM jest krytycznie zależne od odstępów międzykanałowych i dyspersji chromatycznej. Dyspersja chromatyczna zapewnia niedopasowanie fazy między produktami FWM a sygnałami oryginalnymi i łagodzi przesłuchy FWM. Z tego powodu **w systemach wielokanałowych (WDM) wymagana jest niezerowa dyspersja chromatyczna**. Na regularnej siatce DWDM produkty FWM mogą nakładać się na oryginalne kanały, stając się źródłem przesłuchów. Liczba produktów FWM rośnie gwałtownie wraz z liczbą kanałów.

### Chirped pulse vs negative/positive CD

Impuls optyczny jest "ćwierkany" (chirped), gdy jego częstotliwość zmienia się w czasie. Ćwierkanie impulsu może być postrzegane jako źródło różnych komponentów widmowych. Ćwierkanie przyczynia się do poszerzenia impulsu spowodowanego dyspersją chromatyczną. Kształtowanie "ćwierkania" impulsu może być użyte do kompensacji dyspersji chromatycznej. Na przykład, pre-chirping (w nadajniku) może być realizowany za pomocą niezbalansowanego modulatora Mach-Zehndera lub przez modulację częstotliwości (FM). Odpowiednie połączenie znaku "ćwierkania" impulsu (κ) i znaku parametru dyspersji β2​ (związanego ze współczynnikiem Dch​ i jego zależnością od częstotliwości/długości fali) może zoptymalizować propagację. W paśmie 1550 nm dla standardowego światłowodu jednomodowego (G.652) β2​<0 i Dch​>0. Aby zmniejszyć poszerzenie impulsu, ćwierkanie powinno mieć przeciwny znak niż β2​, czyli κ>0. W systemach z negatywną dyspersją (np. w DCF), gdzie Dch​<0, β2​>0, optymalizacja następuje, gdy κ<0.

### OTDR – zasada działania, błędy pomiarowe, parametry OTDR

OTDR (Optical Time Domain Reflectometer) to przyrząd do pomiaru światłowodów. Działa na zasadzie wysyłania impulsu światła w światłowód i analizy odbitego lub rozproszonego sygnału powracającego w czasie. Pozwala na pomiar strat na złączach, spawach, wykrywanie uszkodzeń oraz profilowanie tłumienia wzdłuż światłowodu. Kluczowe parametry OTDR to: zakres dynamiczny (związany z długością impulsu), strefa martwa (dead zone) zdarzeń i tłumienia, rozdzielczość przestrzenna oraz czas uśredniania.

### Test RFC 2544

RFC 2544 definiuje metodologię pomiarów wydajności (benchmarking) dla sieci Ethernet (np. w sieciach optycznych). Są to testy poza usługą (out-of-service). Standard określa rozmiar ramek, czas trwania testu i liczbę iteracji. Główne testy to:

- **Przepustowość (throughput)**: Maksymalna liczba ramek na sekundę, które mogą być przesłane bez strat. Metoda prób i błędów, powtarzana dla różnych rozmiarów ramek (64, 128, ..., 1518 bajtów).
- **Back-to-back**: Ocenia zdolność buforowania przełącznika. Mierzy maksymalną liczbę ramek odebranych z pełną prędkością liniową przed utratą ramki.
- **Straty ramek (frame loss)**: Mierzy, czy sieć zgubiła ramki. Powtarzane przy niższych prędkościach, aż brak strat wystąpi przez trzy kolejne iteracje.
- **Opóźnienie (latency)**: Mierzy czas potrzebny na przejście ramki od urządzenia źródłowego do docelowego w sieci. Testy RFC 2544 mogą być wykorzystywane do oceny sieci optycznych Ethernet. Alternatywą dla RFC 2544 jest Y.1564 (EtherSAM), który mierzy dodatkowe parametry, takie jak zmienność opóźnienia ramek (FDV).

### Pomiary dyspersji: modalnej, chromatycznej i polaryzacyjnej

- **Dyspersja międzymodowa (zniekształcenia)**: Pomiary mogą być wykonywane metodą poszerzenia impulsu (pulse broadening method).
- **Dyspersja chromatyczna (CD)**: Metody obejmują pomiary różnicowe w dziedzinie czasu (Differential time domain measurements), metody testowe przesunięcia fazowego (Phase shift test methods) oraz analizę widma optycznego (Optical spectrum analysis).
- **DGD (PMD)**: Metody pomiaru PMD (DGD) obejmują metodę opóźnienia impulsu (Pulse delay method), metody interferometryczne (Interferometric methods) oraz ocenę parametrów Stokesa (Stokes Parameter Evaluation – Poincaré Arc Method).

### Typy laserów półprzewodnikowych (zasada działania)

Laser to wzmacniacz optyczny zamknięty w rezonatorze (reflective cavity), który powoduje oscylację sygnału ze sprzężeniem zwrotnym dodatnim. Lasery półprzewodnikowe wykorzystują półprzewodniki jako ośrodek wzmacniający. Długość wnęki rezonansowej d określa długości fal, dla których połówki długości fali mieszczą się między lustrami wnęki; te długości fal są wzmacniane.

- **Lasery wielomodowe podłużnie (MLM)**: Emitują światło o kilku długościach fal. Typowym przykładem jest laser Fabry-Perota (FP). Mają szersze widmo.
- **Lasery jednomodowe podłużnie (SLM)**: Emitują światło o jednej dominującej długości fali. Charakteryzują się wysokim współczynnikiem tłumienia modów bocznych (SMSR - Side-Mode Suppression Ratio), typowo > 30 dB. Szerokość widmowa laserów DFB może być bardzo niska (nawet 50 MHz w stabilnym punkcie pracy), ale modulacja bezpośrednia powoduje poszerzenie widma.
    - **Laser DFB (Distributed-Feedback)**: Wykorzystuje falowód z pofałdowaniem w obszarze wzmocnienia, aby uzyskać operację jednomodową. Może być strojony przez zmianę temperatury, ale zakres strojenia pojedynczej wnęki jest ograniczony (typ. poniżej 5 nm). Stosowany w systemach 2,5 Gbps dalekiego zasięgu i 40 Gbps (w modułach CFP).
    - **Laser DBR (Distributed Bragg Reflector)**: Podobny do DFB, ale pofałdowanie jest poza obszarem wzmocnienia. Może być strojony w szerszym zakresie (ponad 40 nm).
    - **Laser VCSEL (Vertical Cavity Surface-Emitting Laser)**: Jest laserem SLM. Są tanie i powszechnie stosowane w systemach transmisji danych. Mają problemy z dużą rezystancją i nagrzewaniem. Zalety to prostsze sprzęganie ze światłowodem, łatwiejsze pakowanie i testowanie, możliwość integracji w macierze wielodługościowe. Stosowany w systemach 1G Ethernet (np. 1000Base-SX na 850 nm).

### Typy fotodetektorów

Fotodetektory zamieniają sygnał optyczny na elektryczny. Fotodioda wykorzystuje złącze p-n półprzewodnika z napięciem wstecznym. Najwyższa długość fali, którą dany półprzewodnik może wykryć, to długość fali odcięcia. Fotodetektor zaprojektowany dla pasma 1550 nm może być używany w oknie 1300 nm.

- **Fotodioda PIN (p-i-n)**: Podstawowy typ fotodetektora.
- **Fotodioda lawinowa (APD - Avalanche Photodiode)**: Zapewnia wewnętrzne wzmocnienie sygnału dzięki efektowi lawinowemu, co zwiększa czułość odbiornika. Odbiornik oparty na APD pracujący w zakresie 1,3-1,6 µm potrzebuje około 700-1000 fotonów na bit dla BER 10⁻⁹.

### Wybrane komponenty fotoniczne: cyrkulator, FBG, MZI

- **Cyrkulatory (Circulators)**: Urządzenia optyczne o trzech lub więcej portach, które kierują światło w określonym kierunku, np. światło wchodzące przez port 1 wychodzi przez port 2, a światło wchodzące przez port 2 wychodzi przez port 3. Są jednokierunkowe.
- **Siatka Bragga w światłowodzie (FBG - Fibre Bragg Grating)**: Okresowe zaburzenie współczynnika załamania światłowodu. Wykonana na krótkim odcinku światłowodu (kilka mm) eksponowanego na światło UV. Odbija światło w wąskim zakresie długości fal (pasmo zaporowe), podczas gdy światło o innych długościach fal przechodzi dalej. Pasmo zaporowe jest zależne od okresu siatki. Stosowana do selekcji operacyjnej długości fali (w laserach SLM), jako filtry optyczne (statyczne/dynamiczne, w OADM, do ochrony laserów) oraz jako **kompensatory dyspersji chromatycznej**. FBG o długości 2,4 m może kompensować CD 80 km linku w oknie 15 nm. Do poprawy jakości (tłumienia listków bocznych) stosuje się siatki apodizowane.
- **Interferometr Mach-Zehndera (MZI)**: Urządzenie wykorzystujące dwie ścieżki optyczne o różnych długościach (opóźnieniach), aby spowodować interferencję fal. Może być wykorzystywany jako modulator optyczny lub **kompensator dyspersji chromatycznej**. W kompensatorze CD opartym na MZI, sygnał jest dzielony i przepuszczany przez dwie ścieżki o różnym opóźnieniu, a następnie rekombinowany, co opóźnia niektóre składowe widmowe i kompensuje dyspersję. Efektywny kompensator wymaga kaskady interferometrów, co powoduje dodatkowe tłumienie.

### Oszacowanie wpływu CD i PMD na wydajność łącza (przykład laboratoryjny)

Wpływ dyspersji chromatycznej i polaryzacyjnej na wydajność łącza (mierzoną np. przez osiągalną prędkość bitową lub maksymalną długość łącza) jest krytyczny, szczególnie przy wyższych prędkościach.

- **Ograniczenie przez CD**: Poszerzenie impulsu spowodowane CD (Δτch​) musi być mniejsze niż pewien ułamek czasu trwania bitu (T=1/B), np. Δτch​<0.306T lub Δτch​<0.491T dla kar 1 dB lub 2 dB odpowiednio. Δτch​ zależy od współczynnika CD (Dch​), szerokości widmowej źródła (Δλ) i długości łącza (L): Δτch​=Dch​⋅Δλ⋅L. Przykład dla systemu 10 Gbps (T=0.1 ns), Dch​=17 ps/nm·km, Δλ=0.2 nm pokazuje, że maksymalna długość łącza ograniczona przez CD wynosi około 25 km dla kary 1dB (lub 16 km dla kary 2dB). W przykładzie budżetu mocy dla 80 km, łącze było zdecydowanie ograniczone przez dyspersję chromatyczną (CD limited).
- **Ograniczenie przez PMD**: Różnicowe opóźnienie grupowe (ΔτPMD​) musi być mniejsze niż pewien ułamek czasu trwania bitu. Na przykład, dla kary 1 dB i dostępności systemu 1 - 4·10⁻⁵, ΔτPMD​<0.1⋅Tbit​. ΔτPMD​ zależy od współczynnika PMD światłowodu (DPMD​) i długości łącza (L), w przybliżeniu ΔτPMD​=DPMD​⋅L![](data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="400em" height="1.08em" viewBox="0 0 400000 1080" preserveAspectRatio="xMinYMin slice"><path d="M95,702
    c-2.7,0,-7.17,-2.7,-13.5,-8c-5.8,-5.3,-9.5,-10,-9.5,-14
    c0,-2,0.3,-3.3,1,-4c1.3,-2.7,23.83,-20.7,67.5,-54
    c44.2,-33.3,65.8,-50.3,66.5,-51c1.3,-1.3,3,-2,5,-2c4.7,0,8.7,3.3,12,10
    s173,378,173,378c0.7,0,35.3,-71,104,-213c68.7,-142,137.5,-285,206.5,-429
    c69,-144,104.5,-217.7,106.5,-221
    l0 -0
    c5.3,-9.3,12,-14,20,-14
    H400000v40H845.2724
    s-225.272,467,-225.272,467s-235,486,-235,486c-2.7,4.7,-9,7,-19,7
    c-6,0,-10,-1,-12,-3s-194,-422,-194,-422s-65,47,-65,47z
    M834 80h400000v40h-400000z"></path></svg>)​ (dla długich światłowodów). Przykład dla systemu 10 Gbps (T=100 ps), DPMD​=0.4 ps/km$^{1/2}$ pokazuje, że łącze jest ograniczone przez PMD do około 83 km, aby spełnić warunek ΔτPMD​<0.1⋅T.

### OTDM (Optical Time Division Multiplexing) – idea, zalety i wady

OTDM to optyczne multipleksowanie z podziałem czasowym. W OTDM, sygnały danych z wielu wolniejszych strumieni są przeplatane w dziedzinie czasu, tworząc jeden szybszy strumień optyczny. Może być używany do transmisji pojedynczego kanału o bardzo wysokiej prędkości (np. do 1 Tbps). Zalety to wysokie prędkości bitowe na pojedynczej długości fali. Wady to skomplikowane multipleksery/demultipleksery optyczne i synchronizacja czasowa na bardzo wysokich prędkościach.

### DWDM vs CWDM vs SWDM

Są to technologie multipleksowania z podziałem długości fali (WDM - Wavelength Division Multiplexing). Umożliwiają przesyłanie wielu kanałów optycznych o różnych długościach fal jednocześnie w jednym światłowodzie.

- **DWDM (Dense Wavelength Division Multiplexing)**: Gęste WDM. Charakteryzuje się wąskimi odstępami międzykanałowymi (np. 12.5 GHz, 25 GHz, 50 GHz, 100 GHz). Umożliwia upakowanie dużej liczby kanałów (typ. 40, 80, a nawet więcej) w ograniczonym paśmie optycznym, np. w paśmie C (1530-1565 nm, ~4 THz) lub L (1565-1625 nm, ~7 THz). Stosowany głównie w sieciach dalekiego zasięgu (long-haul) i metropolitalnych. Wymaga precyzyjnych laserów (SLM DFB) i filtrów (AWG, FBG) oraz zarządzania dyspersją i efektami nieliniowymi.
- **CWDM (Coarse Wavelength Division Multiplexing)**: Szerokie WDM. Charakteryzuje się szerszymi odstępami międzykanałowymi niż DWDM (np. 20 nm). Umożliwia budowę bardziej opłacalnych systemów dzięki zastosowaniu nierestrykcyjnie chłodzonych laserów (uncooled lasers), szerszych tolerancji na długość fali laserów i szerokopasmowych filtrów. Stosowany głównie w sieciach metropolitalnych. Wymaga mniej kanałów niż DWDM ze względu na szersze odstępy i ograniczenia wynikające z tłumienia światłowodu (np. water peak).
- **SWDM (Short Wavelength Division Multiplexing)**: WDM w paśmie krótkofalowym. Stosowany w światłowodach wielomodowych (np. OM5) w paśmie 850-940 nm (850, 880, 910, 940 nm). Umożliwia zwiększenie przepustowości na istniejącej infrastrukturze MMF.

### OSNR-Q-factor-BER (definicje i pomiary)

- **BER (Bit Error Rate)**: Współczynnik błędu bitowego. Jest to stosunek liczby bitów odebranych błędnie do całkowitej liczby przesłanych bitów. Jest podstawową miarą jakości cyfrowego systemu transmisyjnego. Pomiar BER ze 100% pewnością wymaga nieskończonej liczby przesłanych bitów, dlatego często stosuje się testowanie BER z określonym poziomem ufności (np. 95%). BER można oszacować na podstawie pomiarów OSNR i/lub jittera.
- **OSNR (Optical Signal to Noise Ratio)**: Optyczny stosunek sygnału do szumu. Jest powszechnie stosowany do oceny jakości wzmacnianych optycznie systemów DWDM. Dominującym źródłem szumu w takich sieciach są wzmacniacze optyczne (np. EDFA). OSNR można mierzyć za pomocą analizatora widma optycznego (OSA).
- **Q-factor**: Jest miarą jakości sygnału na poziomie elektrycznym, często używaną do oceny wydajności sieci optycznych. Q-factor jest proporcjonalny do OSNR i zależy od optycznej i elektrycznej szerokości pasma odbiornika. Można go mierzyć lub oszacować na podstawie pomiarów OSNR i/lub jittera. BER jest bezpośrednio związane z Q-factor: BER≈(1/(Q2π![](data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="400em" height="1.08em" viewBox="0 0 400000 1080" preserveAspectRatio="xMinYMin slice"><path d="M95,702
    c-2.7,0,-7.17,-2.7,-13.5,-8c-5.8,-5.3,-9.5,-10,-9.5,-14
    c0,-2,0.3,-3.3,1,-4c1.3,-2.7,23.83,-20.7,67.5,-54
    c44.2,-33.3,65.8,-50.3,66.5,-51c1.3,-1.3,3,-2,5,-2c4.7,0,8.7,3.3,12,10
    s173,378,173,378c0.7,0,35.3,-71,104,-213c68.7,-142,137.5,-285,206.5,-429
    c69,-144,104.5,-217.7,106.5,-221
    l0 -0
    c5.3,-9.3,12,-14,20,-14
    H400000v40H845.2724
    s-225.272,467,-225.272,467s-235,486,-235,486c-2.7,4.7,-9,7,-19,7
    c-6,0,-10,-1,-12,-3s-194,-422,-194,-422s-65,47,-65,47z
    M834 80h400000v40h-400000z"></path></svg>)​))⋅exp(−Q2/2). Aby zapewnić określony BER (np. 10⁻¹²), wymagany jest minimalny Q-factor. Dla wyższych prędkości bitowych (np. 40G vs 10G) wymagany jest wyższy OSNR.

### EDFA (Erbium Doped Fiber Amplifier) – zasada działania

EDFA to wzmacniacz optyczny domieszkowany erbem, fundamentalny komponent długodystansowych sieci WDM. Oferuje duże wzmocnienie optyczne w szerokim paśmie widmowym (szczególnie w paśmie C i L), wprowadzając jednocześnie dodatkowy szum (szum samoistnej emisji wzmocnionej - ASE - Amplified Spontaneous Emission). Zasada działania opiera się na zjawisku emisji wymuszonej. EDFA wykorzystuje światłowód domieszkowany jonami erbu (Er³⁺) jako ośrodek aktywny. Zasilanie (pompowanie optyczne) jest dostarczane przez dodatkowe lasery pompujące (np. 980 nm i/lub 1480 nm), które wzbudzają jony erbu do wyższych poziomów energetycznych. Gdy fotony sygnału optycznego o odpowiedniej długości fali (np. w paśmie C) przechodzą przez światłowód domieszkowany erbem, mogą stymulować wzbudzone jony erbu do przejścia na niższy poziom energetyczny, emitując dodatkowe fotony o tej samej długości fali i fazie co fotony sygnału - w ten sposób sygnał jest wzmacniany. Pompowanie przy 980 nm jest bardziej efektywne niż przy 1480 nm. EDFA zazwyczaj pracuje w trybie nasycenia (saturation mode), gdzie wzrost mocy sygnału wejściowego powoduje spadek wzmocnienia. Aby uzyskać płaską charakterystykę wzmocnienia w całym paśmie roboczym (gain equalization), stosuje się filtry optyczne, attenuatory lub specjalne światłowody.

### EDFA (mis)konfiguracja

Źródła nie opisują wprost "mis)konfiguracji" EDFA. Można jednak wywnioskować, że niepoprawna konfiguracja może obejmować:

- Niewłaściwe ustawienie mocy pompowania, co może prowadzić do niewystarczającego wzmocnienia lub nadmiernego szumu ASE.
- Brak odpowiedniego kształtowania charakterystyki wzmocnienia (gain equalization), co skutkuje nierównomiernym wzmocnieniem różnych kanałów WDM, pogarszając OSNR niektórych kanałów.
- Niewłaściwe użycie wzmacniaczy (np. wzmacniacza mocy zamiast przedwzmacniacza, który jest zoptymalizowany pod kątem szumu) w różnych miejscach linku optycznego.
- Kaskadowanie wzmacniaczy bez uwzględnienia ich wrażliwości na temperaturę i moc wejściową.

### Kompensacja CD (światłowód kompensujący, FBG, inne)

Dyspersja chromatyczna (CD) poszerza impulsy, ograniczając prędkość bitową i/lub zasięg łącza. Aby to skompensować, stosuje się różne metody.

- **Kompensacja w nadajniku**: Pre-chirping (np. za pomocą modulatora Mach-Zehndera) lub kształtowanie widma.
- **Kompensacja liniowa (inline)**: Może być umieszczona na początku, końcu lub rozłożona wzdłuż linii (np. przy wzmacniaczach EDFA).
    - **Światłowody kompensujące dyspersję (DCF - Dispersion Compensating Fibre)**: Światłowody zaprojektowane z negatywnym współczynnikiem dyspersji chromatycznej, aby kompensować pozytywną dyspersję standardowych światłowodów (G.652). DCF są zazwyczaj słabo prowadzące, a mod propaguje w dużym stopniu w płaszczu, gdzie składowe widmowe propagują szybciej. Wadą DCF są zazwyczaj wyższe straty sygnału (np. 0.35 dB/km dla -100 ps/nm·km) i większa wrażliwość na gięcia. Pomimo wad, DCF są stosowane w sieciach, czasem jako połowa włókien w kablu z włóknami NZ-DSF (G.655).
    - **Komponenty oparte na interferometrach (Mach-Zehnder) lub siatkach Bragga (FBG)**: Te dyskretne komponenty wprowadzają opóźnienia zależne od długości fali, kompensując CD. FBG o długości 2,4 m może kompensować CD 80 km linku w oknie 15 nm. Kompensatory te mogą wprowadzać dodatkowe tłumienie.
- **Inne metody**: Konjugacja fazowa (Phase-conjugation, spectral inversion technologies). Urządzenie odwracające widmo (spectrum inverting device) jest instalowane w środku linku; druga połowa linku działa na odwrócony sygnał w ten sam sposób, co pierwsza, co efektywnie kompensuje CD. Urządzenia te są jednak złożone i mogą być trudne do umieszczenia w środku linku.
- **Kompensacja w odbiorniku**: Implementowana za pomocą cyfrowego przetwarzania sygnału (DSP - Digital Signal Processing). Umożliwia elektroniczną kompensację CD (i PMD). Jest to kluczowa technologia dla systemów 40/100+ Gbps z modulacją koherentną.

### 40/100/400 GE (fibre lanes vs WDM lanes)

W interfejsach Ethernet o wysokich prędkościach (40, 100, 400 Gbps) stosuje się różne podejścia do osiągnięcia docelowej prędkości poprzez podział strumienia danych.

- **Wykorzystanie wielu włókien (fibre lanes)**: Strumień danych jest dzielony na kilka wolniejszych strumieni, z których każdy jest przesyłany przez oddzielne włókno.
    - **40GBASE-SR4**: 40 Gbps na 4 parach włókien MMF (OM3 lub OM4) na odległość do 100 m (OM3: 70m, OM4: 100m). Każda "linia" (lane) transmituje z prędkością 10,3125 Gbps. Nie używa WDM.
    - **100GBASE-SR10**: 100 Gbps na 10 parach włókien MMF (OM3 lub OM4) na odległość do 100 m (OM3: 70m, OM4: 100m). Każda "linia" transmituje z prędkością 10,3125 Gbps. Nie używa WDM.
    - **100GBASE-SR4**: 100 Gbps na 4 parach włókien MMF (OM3 lub OM4) na odległość do 100 m. Każda "linia" transmituje z prędkością 25 Gbps.
    - **100GBASE-SR2**: 100 Gbps na 2 parach włókien MMF (OM3 lub OM4) na odległość do 100 m. Każda "linia" transmituje z prędkością 50 Gbps.
    - **100GBASE-nR4**: 100 Gbps na 4 włóknach SMF równolegle na odległość do 500 m.
- **Wykorzystanie WDM (WDM lanes)**: Strumień danych jest dzielony na kilka wolniejszych strumieni, z których każdy jest modulowany na innej długości fali i wszystkie są przesyłane w jednym włóknie (lub parze włókien).
    - **40GBASE-LR4**: 40 Gbps na 4 długościach fal (CWDM 20 nm spacing) w jednym włóknie SMF (G.652/G.657) na odległość do 10 km.
    - **100GBASE-LR4**: 100 Gbps na 4 długościach fal w jednym włóknie SMF. Każdy strumień transmituje z prędkością 25,78125 Gbps. Zasięg do 10 km.
    - **100GBASE-ER4**: 100 Gbps na 4 długościach fal w jednym włóknie SMF. Zasięg do 30 km (40 km dla "engineered links"). Wymaga lepszej czułości odbiornika niż LR4.
    - **100GBASE-DR**: 100 Gbps na 1 długości fali (1310 nm) w jednym włóknie SMF na odległość do 500 m.
    - **40GBASE-ER4**: 40 Gbps na 4 długościach fal na odległość do 40 km SMF.

### Kluczowe właściwości OTN (Optical Transport Network)

OTN (ITU-T G.709) to technologia transportu optycznego, która definiuje cyfrowe opakowanie (digital wrapping) strumieni klienta (np. Ethernet, IP) w jednostki ODU (Optical Data Unit). OTN wprowadza hierarchię transportu optycznego (OTH - OTN hierarchy): Physical Media Layer, OTS Layer (Optical Transmission Section), OMS Layer (Optical Multiplex Section), OCh Layer (Optical Channel). OCh Layer obejmuje cyfrowe opakowanie (ODUk, OPUk) i superwizję (OTUk/OTUkV). ODUk zapewnia adaptację sygnałów klienta, superwizję ścieżki end-to-end (ODUkP) i monitorowanie połączeń tandemowych (ODUkT). Jednostki ODUk mają zdefiniowane prędkości dla różnych sygnałów klienta (np. ODU1 dla 2.5 Gbps, ODU2 dla 10 Gbps, ODU3 dla 40 Gbps, ODU4 dla 100 Gbps), istnieje również ODUflex dla elastycznych prędkości. Kluczowe funkcje OTN to: enkapsulacja ramkami i pakietami, monitorowanie wydajności, kontrola błędów (w tym FEC - Forward Error Correction), adaptacja prędkości, mechanizmy multipleksowania, ochrona i odtwarzanie sieci. OTN (w połączeniu z ASON, GMPLS, SDN) umożliwia dynamiczne świadczenie usług transportowych (switched OTN).

### RWA (Routing and Wavelength Assignment) i problem ciągłości długości fali

RWA to algorytm wykorzystywany w planowaniu i dynamicznym zestawianiu ścieżek optycznych (lightpaths) w sieciach WDM. Polega na wybraniu trasy (Routing) i przypisaniu wolnej długości fali (Wavelength Assignment) dla danego połączenia. Kluczowa różnica między routingiem IP a optycznym polega na **ograniczeniu ciągłości długości fali (wavelength continuity)**. Oznacza to, że w sieciach bez konwerterów długości fal, ścieżka optyczna musi wykorzystywać tę samą długość fali na całej swojej trasie. Istnieją różne podejścia do RWA:

- **Najpierw przypisanie długości fali, potem routing (Wavelength Assignment then Routing)**: Wybieramy długość fali (np. pierwszą dostępną, losową, najmniej/najbardziej używaną) i szukamy trasy, na której ta długość fali jest wolna. Proste, ale może być nieefektywne.
- **Najpierw routing, potem przypisanie długości fali (Routing then Wavelength Assignment)**: Najpierw znajdujemy trasę (np. najkrótszą) i sprawdzamy, czy na tej trasie dostępna jest jakakolwiek ciągła długość fali. Jeśli nie, sprawdzamy trasy alternatywne lub możliwość konwersji długości fali (O/E/O lub O/O/O) w węzłach (translucent nodes).
- **Zintegrowane RWA (Integrated Routing and Wavelength Assignment)**: Algorytm routingu jest świadomy dostępności długości fal i możliwości konwersji w węzłach. Może modelować sieć w sposób, który uwzględnia te ograniczenia, np. traktując możliwości konwersji jako "wirtualne linki" o określonym koszcie. Wymaga aktualnej informacji o stanie sieci.

### ROADM (Reconfigurable Optical Add-Drop Multiplexer) – colorless i directionless + architektury

ROADM to konfigurowalny multiplekser add-drop optyczny, kluczowy komponent elastycznych sieci optycznych. Pozwala na dynamiczne dodawanie (add), przepuszczanie (express) i usuwanie (drop) kanałów WDM bez konieczności ręcznej rekonfiguracji sprzętowej.

- **Architektury ROADM**:
    - **Fixed OADM**: Starsze rozwiązanie wykorzystujące stałe filtry (np. FBG), brak elastyczności, wymaga modyfikacji sprzętu do rekonfiguracji.
    - **Demux-Switch-Mux**: Pierwsze rozwiązanie rekonfigurowalne. Demultipleksuje wszystkie kanały WDM, kieruje je do przełącznika optycznego dla każdej długości fali, a następnie remultipleksuje. Porty add/drop muszą być "kolorowe" (przypisane do konkretnej długości fali).
    - **Broadcast and Select**: Wykorzystuje przełączniki selekcji długości fali (WSS - Wavelength Selective Switches). WSS blokuje propagację fal do usunięcia w węźle. Redukuje liczbę komponentów, ale porty add/drop nadal mogą być "kolorowe".
    - **Colourless (Bezkolorowe)**: Umożliwia skierowanie dowolnej długości fali z linii WDM do dowolnego portu add/drop. Osiągnięte dzięki wykorzystaniu WSS, który jest bezkolorowy (nie przypisany do konkretnej długości fali jak demultiplekser AWG). Duża zaleta to możliwość terminacji dowolnej długości fali na dowolnym porcie.
    - **Directionless (Bezkierunkowe)**: Rozszerzenie ROADM, w którym sygnał optyczny może być rozdzielany do wszystkich "kierunków" (portów liniowych). Zadanie add/drop nadal opiera się na WSS. Zwiększa elastyczność węzła.
    - **Contentionless (Bezkolizyjne)**: Zapewnia, że wiele sygnałów o tej samej długości fali może być dodawanych lub usuwanych jednocześnie bez wzajemnych kolizji. (Choć źródła nie wchodzą w szczegóły tej funkcji, wspominają o architekturach CDC - Colorless, Directionless, Contentionless).

Kluczowe parametry ROADM to liczba portów światłowodowych (stopień węzła), liczba długości fal na włókno i maksymalny stosunek add/drop. ROADMy muszą skalować od 2 do 8 par włókien, z 40-96 falami na włókno. Stosunek add/drop zazwyczaj skaluje się do 100% dla mniejszych węzłów (2-4 pary) i do 50% dla większych.

### EON (Elastic Optical Network) (w tym flexgrid) – właściwości, porównanie do WDM

Tradycyjne sieci DWDM są oparte na stałym planie długości fal (siatce częstotliwości) i zazwyczaj wszystkie kanały przenoszą ruch o tej samej prędkości bitowej. W obliczu szybkiej ewolucji interfejsów Ethernet (40G/100G/400G+) i potrzeby transportu ruchu o różnej granularności (od 100 Mbps do 100 Gbps i więcej) potrzebne jest bardziej elastyczne podejście. **Elastic Optical Network (EON)** wprowadza elastyczny plan alokacji widma (flexgrid). Zamiast sztywno zdefiniowanych kanałów o stałej szerokości, EON pozwala na przydział widma o zmiennej szerokości ("slotów") w zależności od potrzeb danego połączenia i zastosowanej modulacji. Umożliwia to efektywniejsze wykorzystanie dostępnego pasma optycznego i bardziej elastyczne dostosowanie przepustowości do wymagań różnych usług. W EON stosuje się elastyczne schematy modulacji, dopasowując je do warunków propagacji i wymaganej przepustowości. Algorytmy Routing and Spectrum Assignment (RSA) są wykorzystywane do alokacji tras i widma w EON.

### OBS (Optical Burst Switching) – idea, planowanie zasobów

OBS to technologia przełączania optycznego, która znajduje się pomiędzy przełączaniem kanałów optycznych (OCh switching) a przełączaniem pakietów optycznych (OPS - Optical Packet Switching). Została zaproponowana, aby uzyskać statystyczny zysk z transmisji datagramowej na poziomie optycznym, jednocześnie radząc sobie z brakiem technologii buforów optycznych i trudnościami w przetwarzaniu nagłówków pakietów optycznych z prędkościami liniowymi. **W OBS, dane są grupowane w "bursty" (wiązki) w węzłach brzegowych**. Nagłówek burstu (control packet) jest oddzielany od ładunku (packet payload). Nagłówek jest wysyłany wcześniej (z pewnym opóźnieniem - offset time) do węzłów rdzeniowych przez dedykowany kanał sterujący. Węzły rdzeniowe przetwarzają nagłówek (elektrycznie), planują zasoby sieciowe (trasę, długość fali) i konfigurują przełączniki optyczne przed nadejściem burstu. Sam burst przechodzi przez sieć optycznie, bez konwersji O/E/O w węzłach rdzeniowych, wykorzystując zaplanowane zasoby. OBS zazwyczaj nie zestawialą połączeń przed wysłaniem pojedynczych burstów. Węzły brzegowe są odpowiedzialne za montaż burstów, klasyfikację QoS, tworzenie nagłówków i oszacowanie offset time. Węzły rdzeniowe odpowiadają za przełączanie burstów, planowanie zasobów i rozwiązywanie kolizji. Kolizje (contention) występują, gdy wiele burstów potrzebuje dostępu do tych samych zasobów jednocześnie. Mogą być rozwiązywane za pomocą linii opóźniających (Fibre Delay Lines - FDL), routingu z defleksją, konwersji długości fali, segmentacji burstu lub algorytmów hybrydowych. Scheduler w węźle rdzeniowym odpowiada za efektywne wykorzystanie zasobów. Algorytmy planowania zasobów, np. Latest Available Unscheduled Channel (LASC) z lub bez wypełniania pustych przestrzeni (void filling), są kluczowe dla wydajności OBS. Mimo badań i testów, technologia OBS wciąż czeka na komercyjne wdrożenie.

### FTTH (Fibre To The Home) – architektury, zasada działania (PON)

FTTH to architektura sieci dostępowej, w której światłowód dociera bezpośrednio do lokalu klienta. Jest częścią szerszej kategorii FITL (Fibre In The Loop). Kluczowe elementy architektury FTTH to: OLT (Optical Line Termination) w centrali operatora, ODN (Optical Distribution Network) - sieć światłowodowa (pasywna lub aktywna) z elementami rozdzielającymi (splitters), ONUs/ONTs (Optical Network Unit/Termination) u klienta. ODN może być:

- **AON (Active Optical Network)**: Wykorzystuje aktywne elementy (np. przełączniki, multipleksery) w sieci dystrybucyjnej. Często oparte na architekturze punkt-punkt (P2P), np. z wykorzystaniem Ethernetu.
- **PON (Passive Optical Network)**: Wykorzystuje wyłącznie pasywne elementy (światłowody, splittery) w sieci dystrybucyjnej. Jeden port OLT obsługuje wielu klientów przez rozgałęziającą się sieć światłowodów i splitterów. W PONach, w kierunku od klienta do centrali (upstream), stosuje się multipleksowanie z podziałem czasowym (TDMA), gdzie OLT przydziela poszczególnym ONU/ONT szczeliny czasowe na transmisję. W kierunku od centrali do klienta (downstream), OLT wysyła dane do wszystkich ONU/ONT (broadcast), a dane dla konkretnego klienta są identyfikowane (np. przez PLOAM grants w BPON) i deszyfrowane. Proces identyfikacji ONU i pomiaru odległości (opóźnienia) nazywa się rangingiem.

### GPON (Gigabit-capable Passive Optical Network) – ogólne właściwości, alokacja widma

GPON (ITU-T G.984) to technologia PON zdolna do gigabitowych prędkości. Jest rozwinięciem specyfikacji BPON (G.983).

- **Prędkości**: Nominalne prędkości liniowe GPON to 1.2 Gbit/s i 2.4 Gbit/s w dół (downstream) oraz 155 Mbit/s, 622 Mbit/s, 1.2 Gbit/s i 2.4 Gbit/s w górę (upstream).
- **Alokacja widma (długości fal)**: W GPON transmisja w górę (upstream) odbywa się zazwyczaj w paśmie 1260-1360 nm (często "narrow band" 1300-1320 nm lub "enhanced" 1290-1330 nm dla 2.5G GPON), a w dół (downstream) w paśmie 1480-1500 nm. Pasmo 1550-1560 nm jest zarezerwowane dla usług wideo (G.983.3).
- **Zasięg i podział**: Maksymalny zasięg logiczny wynosi 60 km (z regeneratorami/wzmacniaczami, standardowy maks. zasięg fizyczny to 20 km). Maksymalny podział (splitting ratio) to 1:64 (potencjalnie 1:128). Maksymalna różnica odległości między najbliższym a najdalszym ONU od OLT wynosi 20 km, z możliwością rozszerzenia do 40 km.
- **Klasy PON**: GPON definiuje klasy PON (A, B, C, B+, C+) w oparciu o minimalne i maksymalne tłumienie w sieci optycznej. Klasy N1, N2, E1, E2 są zdefiniowane dla XG-PON/XGS-PON.
- **Warstwa konwergencji transmisji (TC)**: G.984.3 definiuje warstwę TC, odpowiedzialną za ramkowanie danych (GEM - Gigabit Encapsulation Mode), protokół MAC (TDMA w upstream), komunikaty sygnalizacyjne, ranging, OAM i bezpieczeństwo. GEM wykorzystuje 12-bitowe pole Port_ID. Przydział pasma jest sterowany przez OLT, które przydziela ONU szczeliny czasowe na transmisję w górę.
- **Bezpieczeństwo**: W kierunku downstream, dane są szyfrowane (churned) za pomocą klucza przesyłanego w górę przez ONT, co zapewnia bezpieczeństwo point-to-point.

### TWDM PON (MW-PON)

TWDM PON (Time and Wavelength Division Multiplexing Passive Optical Network) to rozwiązanie PON wykorzystujące wiele długości fal (MW-PON - Multiple Wavelength PON). Każda długość fali jest dzielona między wiele ONU przy użyciu multipleksowania z podziałem czasowym (TDMA). TWDM PON jest kluczową technologią dla NG-PON2 (G.989), następnej generacji PON o prędkości 40 Gbps. Systemy NG-PON2 mogą wykorzystywać 4-8 par kanałów TWDM (downstream i upstream). Nominalne prędkości liniowe na kanał mogą wynosić 10/10 Gbit/s, 10/2.5 Gbit/s lub 2.5/2.5 Gbit/s. Wymagany jest zasięg pasywny co najmniej 40 km i maksymalna różnica odległości do 40 km, z możliwością osiągnięcia 60 km i podziału 1:256. Systemy MW-PON (G.9802) mogą wykorzystywać również wiele par kanałów o prędkości 10 Gbit/s lub 25 Gbit/s na długość fali. Wymagają one laserów strojonych w paśmie DWDM (np. lasery strojone termicznie) oraz urządzeń z różną prędkością strojenia (slow, middle, fast).