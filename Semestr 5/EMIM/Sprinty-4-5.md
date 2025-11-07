# Wstęp
Po 2 tygodniach pracy prezentujemy rezultaty sprintów 4tego i 5tego. Na wstępie wspomnę o pierwotnym planie, ze Sprintu 3ciego:
1. Stworzenie Ścisłych Ograniczeń
2. Uporządkowanie Struktur
3. Implementacja Pełnej Bazy Kart
4. Minimalne Rozszerzenie Zasad
5. Cel Obserwacji
Podczas prac doszliśmy do wniosku, że założenia na te sprinty nie były odpowiednie. Skupiliśmy się na automatyzacji i jej testowaniu. 
# Sprint 4 - Interfejs
# Wstęp
Podczas pisania interfejsu do gry, w celu automatyzacji i ustandaryzowaniu talii, doszliśmy do wniosku, że to jest prawidłowy kierunek rozwoju. Skrócenie czasu gry przez polepszenie systemu generowania promptów pozwoli nam, na dłuższą metę, na szybszą pracę. Cały ten tydzień poświęciliśmy na odwzorowanie wielu mechanik w interfejcsie, przez co można powiedzieć, że prawie stworzyliśmy silnik do gry w Diunę.
## README

> # Asystent Gry Dune: Imperium (Dune: Imperium Game Assistant)
> 
> ## Opis Projektu
> 
> **Asystent Gry Dune: Imperium** to aplikacja webowa (oparta na Flask), która służy jako cyfrowy pomocnik do zarządzania fizyczną grą planszową _Dune: Imperium_.
> 
> Nie jest to pełna, automatyczna implementacja gry. Jest to narzędzie stworzone, aby ułatwić graczom śledzenie złożonego stanu gry, automatyzować niektóre obliczenia i wspierać rozgrywkę z udziałem "gracza AI" poprzez generowanie dla niego specjalnych promptów.
> 
> Głównym celem aplikacji jest:
> 
> 1. Utrzymywanie "źródła prawdy" (Source of Truth) o stanie gry (zasoby, karty, lokacje).
>     
> 2. Walidacja i logowanie ruchów graczy w Fazie Agentów.
>     
> 3. Automatyczne obliczanie statystyk (Perswazja, Siła) na potrzeby Fazy Odkrycia.
>     
> 4. Generowanie ustrukturyzowanych promptów tekstowych, które można przekazać do zewnętrznego modelu LLM (jak ChatGPT, Gemini, Claude), aby uzyskać sugestię ruchu dla gracza AI.
>     
> 
> ## Kluczowe Funkcje
> 
> - **Zarządzanie Stanem Gry:** Śledzi rundę, fazę, zasoby graczy (Solari, Woda, Przyprawa, Wojsko), wpływy oraz stan lokacji (kto zajął).
>     
> - **Interfejs Fazy Agentów:** Pozwala graczom na wybranie karty z ręki (lub talii dla ludzi) i lokacji docelowej. Aplikacja sprawdza poprawność ruchu (np. czy lokacja jest wolna, czy karta ma odpowiedni symbol, czy gracza stać na koszt).
>     
> - **Logowanie Historii:** Każdy ruch, pas, zagranie intrygi czy ustawienie konfliktu jest logowane w historii rundy.
>     
> - **Interfejs Fazy Odkrycia:** Po zakończeniu Fazy Agentów, aplikacja automatycznie przechodzi do widoku `/reveal`.
>     
>     - Automatycznie oblicza i wyświetla sumę Perswazji i Siły dla wszystkich graczy na podstawie ich zagranych kart i kart na ręce.
>         
>     - Umożliwia ręczne zalogowanie wyników konfliktu (kto zajął które miejsce).
>         
>     - Pozwala na rejestrowanie zakupów z Rzędu Imperium, walidując koszt i dostępną Perswazję.
>         
> - **Generator Promptów AI:** Dedykowana strona (`/ai_prompt`) generuje szczegółowy prompt dla gracza AI (`Peter`). Prompt zawiera:
>     
>     - Aktualny stan gry, nagrody w konflikcie, historię ruchów.
>         
>     - Podsumowanie publicznych informacji o przeciwnikach.
>         
>     - Pełny, ukryty stan gracza AI (ręka, zasoby, intrygi) w formacie JSON, gotowy do analizy przez model językowy.
>         
> - **Zarządzanie Grą:**
>     
>     - Ręczne ustawianie ręki gracza AI (na wypadek, gdyby automatyczne dociąganie nie było pożądane).
>         
>     - Rozpoczęcie nowej rundy (czyści planszę, przesuwa karty, automatycznie dociąga 5 kart dla wszystkich graczy).
>         
>     - Pełny reset gry do stanu domyślnego (`game_stat.DEFAULT.json`).
>         
> 
> ## Technologie
> 
> - **Backend:** Python, Flask
>     
> - **Frontend:** HTML5, CSS, JavaScript (po stronie klienta)
>     
> - **Przechowywanie Danych:** Pliki JSON (dla stanu gry, definicji kart, lokacji i intryg)

## Zasady
Ponadto znaleźliśmy błąd w naszej interpretacji zasad w j. polskim. Zasady anglojęzyczne precyzyjniej opisują tury agentów co spowodowało znaczącą zmianę zasad gry. Doszliśmy do wniosku, że nowicjusz, który przestał nim być w poprzedniej grze, może być użyty do kolejnej rozgrywki.

# Sprint 5 - rozgrywka
# Wstęp
Wykonaliśmy zaplanowaną rozgrywkę, jednak nie pod kątem sprawdzenia dostępu do internetu, lecz troubleshootingu naszego interfejsu. Z powodu niedopracowania systemu, zdarzały się przestoje na naprawę błędów lub niedopatrzeń. Rezultatem są więc nie tylko przemyślenia dotyczącze mistrza gry, lecz także konkretny plan usprawnienia interfejsu.
# Automatyzacja
Interfejs służący nam za narzędzie przyspieszające pracę niestety miał dużo niedopatrzeń takich jak case sensitivity, czy braki implementacji, które dopisywaliśmy na bieżąco. Rozgrywka nie skróciła się tak jak zakładaliśmy lecz wydłużyła do 5,5h. Nie uznajemy tego za porażkę, ponieważ z każdym rozwiązanym problemem usprawnialiśmy system. Ponadto można powiedzieć, że wykonaliśmy testy oprogramowania, przy czym łataliśmy kod w trakcie. Warto wspom nieć, że stworzyliśmy także plan rozwoju interfejsu, dzięki czemu wiemy w jakim kierunku rozwijać program.
## Rozgrywka
Do rozgrywki użyliśmy nowego konta Gemini 2.5 Pro, jest to więc nowicjusz. Zestawiliśmy go z nowicjuszem który grał już w grę, lecz o zmodyfikowanych zasadach.
Zmieniły się prompty jakie używaliśmy. Co ruch Mistrza, generowaliśmy prompt z naszego interfejsu. Przez niedopracowanie systemu podejrzewamy degradację jakości myślenia strategicznego, lecz pracujemy nad raportem z tej rozgrywki.
Mistrz przegrał sromotnie!
# Podsumowanie
Interfejs okazał się narzędziem niezbędnym do dalszego działania. Ma potencjał usprawnienia pracy, co znaczy, że nie jest jeszcze dopracowany. Rozwinął się na ten moment od prostej automatyzacji zagrywania kart, po resurce management, zagrywanie intryg, dobieranie kart na ręce i wiele innych funkcjonalności. Będziemy kontynuować nad nim pracę. 
# Plan na Sprint 6
Realizacja kompletnego interfejsu.

