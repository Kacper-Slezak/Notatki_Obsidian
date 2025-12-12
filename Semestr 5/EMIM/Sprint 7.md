# Raport z Podsumowania Sprintu 7: Weryfikacja Ciągłości Strategicznej AI i Stabilizacja Systemu

Projekt: Mistrz Gry
## 1. Cel Sprintu

Głównym celem sprintu było przeprowadzenie pełnej, kontrolowanej rozgrywki z wykorzystaniem modelu AI ("Peter" – Duke Leto Atreides) w środowisku naszego autorskiego interfejsu.

Skupiliśmy się na trzech aspektach:

1. **Weryfikacja potencjału:** Czy model językowy jest w stanie grać na poziomie zaawansowanym, gdy otrzyma odpowiednie dane?

2. **Testy obciążeniowe:** Sprawdzenie stabilności interfejsu i wychwycenie błędów logicznych w trakcie "żywej" rozgrywki.

3. **Analiza ciągłości:** Zidentyfikowanie momentów, w których AI zmienia lub traci swoją strategię.

## 2. Rozwój Aplikacji i Przebieg Testów

Aplikacja przeszła chrzest bojowy. W trakcie wielogodzinnej sesji zidentyfikowano szereg błędów 
(_edge cases_), które wymagały natychmiastowej interwencji.

- **Działania:** Zespół wprowadzał poprawki do kodu backendu w czasie rzeczywistym.

- **Efekt:** Choć wydłużyło to czas sesji, pozwoliło na **trwałe uszczelnienie logiki gry**. System jest teraz znacznie bardziej odporny na błędy i gotowy do kolejnych testów.

## 3. Przebieg Rozgrywki i Analiza AI

Uczestnicy: AI (Peter) vs. Tymon (Weteran) vs. Damian (Nowicjusz).

Wynik: AI zajęło 2 miejsce.

### A. Sukcesy:

W początkowej fazie gry AI zaprezentowało poziom, który potwierdza słuszność obranego kierunku rozwoju:

- **Zrozumienie Ekonomii:** W _Rundzie 1_ AI podjęło decyzję o odpuszczeniu niepewnego konfliktu militarnego na rzecz budowy ekonomi, co zapewniło mu stabilność w środkowej części gry.

- **Zrozumienie Atutów Lidera:** Model bezbłędnie interpretował pasywne zdolności Duke'a Leto. W _Rundzie 2_ wykorzystał zniżkę Landsraadu, by zdobyć Mentata (dodatkowego agenta) znacznie taniej niż przeciwnicy.

- **Świadomy Deck-Building:** Ruch na pole _Selective Breeding_ w celu usunięcia słabej karty startowej i dobrania nowych był podręcznikowym przykładem zaawansowanej gry.

To dowodzi, że model – gdy posiada pełny kontekst – potrafi grać optymalnie.

### B. Wyzwanie: "Strategiczna Nieciągłość" (Analiza Degradacji)

W toku analizy logów zidentyfikowaliśmy zjawisko spadku jakości decyzji w czasie. Wynika ono z faktu, że AI otrzymywało w prompcie historię ruchów **tylko z bieżącej rundy**. Model "widział" planszę, ale nie pamiętał swoich długofalowych planów z przeszłości.

Prowadziło to do następujących błędów strategicznych:

1. Syndrom "Zbieracza" (Błąd Deck-buildingu):

	AI nadmiernie kupowało karty średniej jakości (Arrakis Liaison), zamiast oszczędzać na karty kluczowe. W efekcie, w decydujących momentach talia była "rozwodniona" słabszymi kartami.

2. Niewykorzystany Potencjał Ekonomiczny:

    W rundach 4-6 AI generowało potężną ilość Perswazji (nawet 10-11 punktów). Zamiast zamienić to na pewne Punkty Zwycięstwa (kupując The Spice Must Flow), AI rozdrabniało kapitał na kilka tańszych kart, zapominając o celu głównym.

3. Błędna Inwestycja w "Late Game":

    W przedostatniej rundzie AI wydało cenne zasoby na miejsce w High Council. Jest to inwestycja, która zwraca się po wielu rundach – na tym etapie należało skupić się na natychmiastowych punktach.

3. Pasywność Militarna:
    
    AI poprawnie identyfikowało przewagę rywali, ale reagowało całkowitym wycofaniem. Zamiast walczyć o tanie 2. miejsca (dające zasoby), oddawało pole walki za darmo.

3. Amnezja Zasobowa (Intrygi):

    Najpoważniejszy błąd techniczny wystąpił w Rundzie 8. AI zagrało kartę Market Monopoly, będąc przekonanym, że spełnia jej warunki. Okazało się jednak, że model "zapomniał", iż w poprzednich rundach nie zakupił wymaganych kart The Spice Must Flow.

## 4. Wnioski

1. **Diagnoza jest optymistyczna:** AI nie popełniało błędów z braku inteligencji, lecz z braku dostępu do własnej historii ("pamięci długotrwałej"). Jest to problem techniczny, który łatwo rozwiązać.

2. **Degradacja potwierdza brak danych:** Obserwowany spadek jakości gry – od "Grandmastera" w rundach 1-3 do błędów kontekstowych w rundach 7-8 – stanowi bezpośredni dowód na to, że model tracił wątek strategiczny, nie mając wglądu w swoje decyzje z przeszłości.

3. **Konieczność "zszycia" gry:** Aby AI grało jak człowiek przez całą rozgrywkę, musimy wdrożyć mechanizmy przenoszenia kontekstu (planów i historii zakupów) z rundy na rundę.



## 5. Propozycje Ulepszeń i Możliwości Rozwoju

Aby wyeliminować efekt "amnezji" i podnieść poziom rozgrywki, proponujemy wdrożenie któregoś z  usprawnień w promptach.

### Opcja A: "Notatka Strategiczna" 

- **Opis:** Na koniec każdej tury prosimy AI o napisanie jednego zdania podsumowującego plan na przyszłość (np. _"Muszę kupić jeszcze jedną kartę Spice Must Flow"_). Tę notatkę doklejamy do promptu w kolejnej rundzie.

- **Cel:** Utrzymanie ciągłości myśli.

### Opcja B: Wymuszenie "Myślenia Wstecznego" 

- **Opis:** Zanim AI poda ruch, wymuszamy na nim weryfikację własnych zasobów: _"Sprawdź swoje karty Intryg. Czy masz wystarczająco dużo kart w talii, by je zagrać?"_.

- **Cel:** Eliminacja błędów wynikających z przeoczenia szczegółów w JSON-ie.

### Opcja C: Dynamiczne Archetypy Strategiczne

- **Opis:** Danie AI wyboru "osobowości" w trakcie gry (np. _Monopolista_, _Generał_, _Polityk_).

- **Cel:** Ułatwienie AI podejmowania decyzji zakupowych poprzez filtrowanie ich przez wybrany archetyp.

### Opcja D: Inicjalizacja Wiedzą 

- **Opis:** Wstrzyknięcie na początku gry skróconego "poradnika".

- **Cel:** Nadanie rozgrywce właściwego kierunku od pierwszej minuty.

### Opcja E: Wskazówki Fazowe 

- **Opis:** Aplikacja automatycznie dodaje do promptu wskazówkę zależną od etapu gry (np. _"To końcówka gry. Ignoruj inwestycje długoterminowe, kupuj tylko VP"_).

- **Cel:** Zapobieganie nielogicznym inwestycjom w ostatnich rundach.

### Opcja F: Warstwa "Doradcy" (Advisor Layer)

- **Opis:** Podział promptu: najpierw AI jako "Doradca" analizuje sytuację, a potem jako "Gracz" wykonuje ruch.

- **Cel:** Oddzielenie planowania od egzekucji, co możliwie zmniejsza szanse na popełnienie błędu.

## 6. Plan na Sprint 7

1. **Finalizacja Aplikacji:** Wdrożenie ostatnich poprawek stabilności.

2. **Implementacja "Pamięci":** Wybór i wdrożenie któryś z opcji ulepszeń, aby AI grało lepiej

3. **Kolejna Rozgrywka:** Test z wdrożonymi zmianami, ze szczególnym naciskiem na weryfikację, czy AI pamięta swoje plany z poprzednich rund i unika błędów "amnezji".