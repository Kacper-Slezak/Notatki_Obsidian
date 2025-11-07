**Raport z Podsumowania Sprintu 4-5: Izolacja AI, usprawnienie gry, wprowadzenie kart

Projekt: Mistrz Gry

## 1. Wstęp: Zmiana założeń

Na początku tego dwutygodniowego okresu pracy planowaliśmy realizować cele zdefiniowane po Sprincie 3 (ścisłe ograniczenia, uporządkowanie struktur, baza kart).

Jednak po rozpoczęciu prac doszliśmy do wniosku, że pierwotne założenia nie były odpowiednie. Zdecydowaliśmy się całkowicie zmienić fokus i **skupić się na automatyzacji procesu gry, jej testowaniu oraz izolacji AI poprzez dostarczenie mu dostatecznej ilości danych o grze**.

## 2. Tydzień 1 (Sprint 4): Rozwój Interfejsu i Bazy Danych

Pierwszy tydzień w całości poświęciliśmy na stworzenie interfejsu do gry. Celem było ustandaryzowanie talii i automatyzacja, co na dłuższą metę ma skrócić czas rozgrywki przez sprawniejsze generowanie promptów.

W trakcie prac nad interfejsem zespół się podzielił:

- **Część zespołu** programowała aplikację (interfejs webowy oparty na Flask).

- **Druga część zespołu** ręcznie spisywała wszystkie możliwe karty i lokalizacje do gry. Podjęliśmy się tego zadania, ponieważ po kilku dniach poszukiwań nie znaleźliśmy odpowiedniej, gotowej bazy danych.


Ręcznie zmapowaliśmy wszystkie karty i zdecydowaliśmy, że będziemy kontynuować rozgrywkę z AI w języku angielskim. W praktyce stworzylismy niemal kompletny silnik do gry w Diunę.

### Kluczowe Funkcje Opracowanego Interfejsu

Aplikacja pełni rolę cyfrowego pomocnika do zarządzania fizyczną grą. Jej głównym celem **nie jest** pełna implementacja gry, lecz ułatwienie śledzenia stanu i generowanie promptów dla AI.

Najważniejsze funkcjonalności:

- **Źródło Prawdy:** Utrzymywanie aktualnego stanu gry (zasoby, karty, zajęte lokacje).

- **Walidacja Ruchów:** Interfejs Fazy Agentów pozwala graczom wybierać karty i lokacje, sprawdzając poprawność ruchu (np. czy lokacja jest wolna, czy gracza stać na koszt).

- **Automatyzacja Fazy Odkrycia:** Aplikacja automatycznie oblicza sumę Perswazji i Siły dla wszystkich graczy.

- **Generator Promptów AI:** Dedykowana strona (`/ai_prompt`) generuje szczegółowy prompt dla gracza AI (`Peter`), zawierający pełny stan gry, historię ruchów oraz ukryty stan gracza AI (ręka, zasoby) w formacie JSON.

- **Zarządzanie Grą:** Śledzenie rundy, fazy, zasobów, logowanie historii, reset gry, kupowanie kart. 

- **Technologie:** Backend (Python, Flask), Frontend (HTML, CSS, JS), Przechowywanie danych (Pliki JSON).

### Odkrycie Dotyczące Zasad

W trakcie prac znaleźliśmy błąd w naszej interpretacji polskich zasad. Wersja anglojęzyczna precyzyjniej opisuje tury agentów, co doprowadziło do modyfikacji zasad.

## 3. Tydzień 2 (Sprint 5): Rozgrywka Testowa i Analiza AI

W drugim tygodniu wykonaliśmy zaplanowaną rozgrywkę. Jej cel był dwojaki: **troubleshooting naszego nowego interfejsu** oraz **bieżąca analiza strategii i ruchów AI**.

### Przebieg Rozgrywki

- **Konfiguracja:** W rozgrywce wzięło udział trzech graczy:
    
    1. Nowicjusz z poprzedniej gry (człowiek).
    
    2. Doświadczony gracz (człowiek).
    
    3. AI (nowe konto Gemini 2.5 Pro, jako "nowicjusz").

- **Problemy Techniczne:** Interfejs okazał się niedopracowany. Napotkaliśmy lekkie problemy    (np. _case sensitivity_, brakujące implementacje), które musieliśmy naprawiać na bieżąco ręcznie bez automatyzacji w JSON i zapisać jako poprawki na kolejną wersje interfejsu.

- **Czas Gry:** Z powodu przestojów na naprawę błędów, rozgrywka trwała **5 godzin**. Nie udało się jej bardziej zoptymalizować ze względu na niedopracowanie interfejsu i rotacje kadrowe.

- **Wynik Testów:** Mimo długiego czasu, nie uznajemy tego za porażkę. Efektywnie wykonaliśmy testy oprogramowania i "łataliśmy" kod w trakcie użytkowania. Stworzyliśmy także plan dalszego rozwoju interfejsu.


### Kluczowe Obserwacje Dotyczące AI

Analiza ruchów AI przyniosła kilka ciekawych wniosków:

1. **Osiągnięcie Izolacji:** Najważniejszy wniosek. Prawdopodobnie udało nam się osiągnąć cel z poprzedniego sprintu. Dzięki naszemu pełnemu przedstawieniu stanu gry (karty, lokacje, zasoby) w promcie, **AI nie korzystało z internetu** w celu pozyskiwania informacji o zasadach czy gotowych strategiach.

2. **Błędna Strategia (Mentat):** AI obrało dziwną strategię, inwestując bardzo wcześnie w Mentata (zapewniającego dodatkowy ruch). Nasze doświadczenie wykazuje, że jest to ruch opłacalny dopiero w późniejszej fazie gry, przy lepszych kartach na ręce.

3. **Problem z Utratą Kontekstu:** Przez nasze przeoczenie, AI nie otrzymywało pełnej aktualizacji wyniku gry _co prompt_, a jedynie raz na kilka tur. Sprawiło to, że model "gubił się" w sytuacji i **nie był w stanie dostosować strategii do faktu, że wyraźnie przegrywa**.

4. **Ignorowanie Kart Intryg:** Model notorycznie nie wykorzystywał posiadanych kart Intryg, mimo że przypominaliśmy mu o nich. Prawdopodobnie wynikało to z faktu, że interfejs nie prezentował mu tych danych w wystarczająco przystępnym formacie. Stawiało go to od początku na przegranej pozycji względem ludzkich graczy.

5. **Pętla Analityczna (Koniec Gry):** Pod koniec gry, gdy AI zorientowało się, że przegra, zaczęło bardzo mocno analizować wszystkie możliwe ruchy i ich wyniki. Model nie widział nigdzie sukcesu i "zapętlił się", generując bardzo długą odpowiedź. Musieliśmy ręcznie przerwać generowanie.

6. **Wynik:** Mistrz (AI) **przegrał sromotnie**.

## 4. Podsumowanie Sprintów 4 i 5

Interfejs okazał się narzędziem absolutnie niezbędnym do kontynuowania projektu. Chociaż obecnie nie jest jeszcze dopracowany, ma ogromny potencjał usprawnienia pracy. W trakcie tych dwóch tygodni rozwinął się z prostej automatyzacji zagrywania kart do systemu zarządzającego zasobami, intrygami i dobieraniem kart. Praca nad nim będzie kontynuowana.

## 5. Plan na Sprint 6

Plan na kolejny sprint jest jasny i skoncentrowany:
	
1. **Dokończenie kluczowych funkcjonalności aplikacji:**
    
    - Celem jest wyeliminowanie błędów i przestojów zidentyfikowanych w ostatniej rozgrywce.
    
    - Kluczowe jest zagwarantowanie, że interfejs dostarcza **pełny, zaktualizowany stan gry w każdym pojedynczym prompcie**, aby definitywnie rozwiązać "Problem z Utratą Kontekstu".
    
2. **Optymalizacja czasu gry oraz Weryfikacja i wzmocnienie instrukcji systemowych (System Prompt):**
    
    - Celem jest kategoryczne zakazanie AI korzystania z wiedzy zewnętrznej, nawet jeśli napotka luki w danych z interfejsu.
    
    - Docelowy czas rozgrywki to ok. 3 godziny (niewiele dłużej niż standardowa gra na 3 graczy).
    
3. **Rozgrywka:**
    
    - Przeprowadzenie idealnie dopracowanej rozgrywki z dobrze zaizolowanym AI.
    
    - Główny cel to przetestowanie zdolności AI do grania w grę strategiczną, gdy ma do dyspozycji pełne spektrum informacji i możliwości, ale bez dostępu do zewnętrznych strategii.
    
4. **Przeprowadzenie dogłębnej analizy "myśli" i strategii AI:**
    
    - Upewnienie się, że AI otrzymuje idealnie sformatowane i kompletne dane (szczególnie o kartach Intryg) w sposób dla niego przystępny.
    
    - Wznowienie **analizy porównawczej** strategii AI (bazującej tylko na danych) ze strategiami graczy ludzkich (nowicjusza i doświadczonego), co było planowane już w Sprincie 2, ale porzucone w Sprincie 3 z powodu braku izolacji.
    
    - Obserwacja, czy AI jest w stanie podejmować **racjonalne decyzje w obliczu przegranej** (np. minimalizować straty), zamiast wpadać w "Pętlę Analityczną", jak zaobserwowano w ostatniej grze.