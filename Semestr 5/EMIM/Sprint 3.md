**Raport z Podsumowania Sprintu 3: Wstępna Gra w "Dune: Imperium" z AI**

Projekt: Mistrz Gry

### 1. Cel Sprintu

Głównym celem tego sprintu było przeprowadzenie pierwszej, wstępnej rozgrywki w "Dune: Imperium" z modelem językowym (AI). Chcieliśmy uzyskać bazową obserwację, jak model poradzi sobie z interpretacją złożonych zasad, jak będzie reagował na dynamiczny stan gry prezentowany w formacie JSON i jakie decyzje strategiczne podejmie w ramach pierwszej, niekontrolowanej w pełni interakcji.

### 2. Przebieg Eksperymentu

Eksperyment został przeprowadzony poprzez serię ustrukturyzowanych promptów, które symulowały kolejne tury gry:

1. **Inicjalizacja:** Model otrzymał konkretną tożsamość (Peter, grający Jarlem Memnonem Thorvaldem), zestaw startowy oraz jasne instrukcje początkowe, w tym zasady specjalne lidera.
    
2. **Aktualizacje Stanu:** Po ruchach graczy ludzkich (Helen, Paul), AI otrzymywało pełny, zaktualizowany stan gry w formacie JSON oraz opisowe podsumowanie ruchów przeciwników.
    
3. **Podejmowanie Decyzji:** AI było proszone o wykonanie własnych ruchów (Faza Agenta lub Faza Ujawnienia) i zwrócenie ich w wymaganym formacie JSON, poprzedzając to pisemną analizą.
    

### 3. Analiza Interakcji i Decyzji AI

W interakcjach AI trzymał się reguł odpowiadania w formacie JSON, przestrzegał zasad tury (czekał na ruchy, nie próbował stawać na zajętych lub nieistniejących polach).

Niestety, model popełniał wyraźne błędy strategiczne, szczególnie w późniejszej fazie gry:

1. **Nieracjonalne Zarządzanie Konfliktem:** W pewnym momencie, będąc ostatnim graczem i nie mając szans na wygranie konfliktu, AI zaangażowało 4 żołnierzy, zamiast wysłać jednego (minimalizując straty) i skupić się na innych celach.
    
2. **Ignorowanie Limitu Garnizonu:** W przedostatniej rundzie (runda 9), AI pozostawiło 6 żołnierzy w garnizonie. Jest to błąd, ponieważ domyślny limit rekrutacji z garnizonu to 3 jednostki na rundę, a model nie posiadał kart ani zdolności pozwalających ominąć to ograniczenie. Co oznacza, że w ostatniej rundzie z garnizonu nie wyciągnie więcej niż 3 żołnierzy, a w 9 przed ostatniej nie wygrał konfliktu, choć była by na to szansa w przypadku nie pozostawienia takiej ilości żołnierzy w garnizonie bez przyczyny.
    
3. **Błędne Priorytety w Ostatniej Rundzie:** Pod koniec ostatniej rundy AI nie zakupiło dostępnej karty "Przyprawa Musi Płynąć", która gwarantowała 1 Punkt Zwycięstwa. Zamiast tego, błędnie kupowało karty do talii, które nie mogły już zostać użyte, ponieważ gra się kończyła.
    
4. **Halucynacje i Gromadzenie Zasobów:** Zaobserwowano rzadkie, ale znaczące halucynacje dotyczące zdolności kart (dodawanie lub odejmowanie efektów). Model wykazywał również tendencję do nadmiernego gromadzenia zasobów bez wyraźnego planu ich wykorzystania.
    

Podsumowując, AI wykonywało zaskakująco dobre ruchy, bez częstych halucynacji oraz z pewną myślą strategiczną. Z perspektywy analizy samych ruchów (bez wglądu w jego "myśli"), model nie byłby łatwy do odróżnienia od ludzkiego gracza.

### 4. Porównanie Procesu Myślowego AI vs. Gracz Ludzki

Jednym z pobocznych celów sprintu była analiza "procesu myślowego" AI (pisemnych uzasadnień ruchu) i porównanie go z logiką podejmowania decyzji przez nowicjusza.

Zadanie to zostało jednak świadomie porzucone. Głównym powodem był brak faktycznej izolacji modelu AI. Szybko stało się jasne, że AI ewidentnie korzystało ze swojej obszernej wiedzy zewnętrznej (strategii internetowych lub danych treningowych), zamiast opierać się wyłącznie na dostarczonych zasadach i stanie gry.

Ze względu na brak czasu oraz fakt, że "przemyślenia" AI nie były adekwatne do symulowanego środowiska (lecz stanowiły odzwierciedlenie gotowych strategii), dalsza analiza porównawcza została uznana za bezcelową. Porzuciliśmy ją na rzecz priorytetyzacji izolacji AI w kolejnym sprincie.

### 5. Ocena Krytyczna i Główne Wnioski

Zakończony sprint, choć męczący i bardzo czasochłonny (rozgrywka trwała wiele godzin), dostarczył kluczowych wniosków na temat dalszego rozwoju projektu.

- **Problem z izolacją AI:** Najważniejszym wnioskiem jest fakt, że pomimo naszych prób ograniczenia modelu do dostarczonych materiałów, AI i tak korzystało ze swojej obszernej wiedzy wewnętrznej na temat gry i znanych strategii. Nasze próby "zamknięcia" go w naszym systemie były niewystarczające.
    
- **Wyczerpanie Procesem:** Początkowo ręczne wprowadzanie danych, śledzenie stanu gry i reagowanie na ruchy AI okazało się bardzo męczące. Nie mieliśmy idealnie opracowanego podejścia, więc skończyło się początkowo na kilku próbach rozpoczęcia rozgrywki. Udało się jednak opracować w miarę optymalną strategie w trakcie rozgrywki. 
    
- **Ograniczenia Bazy Danych:** Nasza baza kart i zasad była niekompletna. To, w połączeniu z ręcznym wpisywaniem informacji w promptach (co powodowało błędy składniowe i słowne), prawdopodobnie skłaniało AI do "uciekania" w stronę swojej wiedzy ogólnej, zamiast trzymać się naszych danych dotyczących rozgrywki podanych mu na początku.
    

### 6. Plany na Następny Sprint

Bazując na wnioskach z tej iteracji, następny sprint musi skupić się na odzyskaniu kontroli nad środowiskiem testowym.

1. **Stworzenie Ścisłych Ograniczeń:** Kluczowe będzie zaimplementowanie bardzo silnych instrukcji systemowych (System Prompt), które kategorycznie zakażą AI korzystania z wiedzy zewnętrznej i nakażą mu traktowanie naszych plików jako jedynego źródła prawdy.
    
2. **Uporządkowanie Struktur:** Musimy stworzyć bardziej uporządkowaną i rygorystycznie przestrzeganą strukturę danych (np. zasady, opisy kart). Musi być ona kompletna na tyle, aby AI nie "zgubiło się" w sprzecznościach.
    
3. **Implementacja Pełnej Bazy Danych Kart:** Aby wyeliminować halucynacje dotyczące zdolności kart i uniemożliwić AI poszukiwanie informacji w Internecie (gdy napotka luki w naszej bazie), musimy dostarczyć modelowi kompletną i dostępną w kontekście bazę danych wszystkich kart i ich efektów.
    
4. **Minimalne Rozszerzenie Zasad:** Należy nieznacznie rozbudować zestaw zasad, aby pokryć luki zidentyfikowane w tym sprincie, co powinno zmniejszyć liczbę błędów interpretacyjnych.
    
5. **Cel Obserwacji:** Głównym celem będzie obserwacja, jak model zachowa się w tym nowym, znacznie bardziej ograniczonym środowisku – czy zacznie podejmować decyzje czysto logiczne (bazujące tylko na danych), czy też nadal będzie próbował forsować strategie ze swojej wiedzy wewnętrznej. Będziemy również obserwować możliwości strategiczne AI przy braku dostępu do gotowych strategii, jego zdolność utrzymywania kontekstu oraz analizy gry.