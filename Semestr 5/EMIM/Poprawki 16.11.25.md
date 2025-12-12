### A. Błędy Krytyczne i Logika Fazy Agentów

1. **Naprawiono krytyczny błąd logiki `CHOICE`:**
    
    - **Problem:** Kod nie potrafił obsłużyć dwóch różnych struktur JSON dla "wyboru" (jedna dla intryg, druga dla kart/liderów).
        
    - **Poprawka:** Funkcja `_process_action_list` (w `game_manager.py`) została zmodyfikowana, aby poprawnie obsługiwać **obie** struktury. Teraz karty agentów (`firm_grip`, `power_play`), sygnety liderów (`Beast Rabban`) oraz intrygi (`master_of_tactics`) poprawnie uruchamiają okno decyzji.
        
2. **Naprawiono błąd logiki `REQUIREMENT` (problem "atrap"):**
    
    - **Problem:** Funkcja `_check_requirement` (w `game_manager.py`) była "atrapą" i przepuszczała prawie wszystkie warunki (np. "Fremen Bond", "2+ wpływu u Gildii") jako `TRUE`.
        
    - **Poprawka:** Funkcja została całkowicie przepisana. Teraz aktywnie sprawdza stan gry (`game_state`, `discard_pile`, `influence`) i poprawnie blokuje efekty, jeśli gracz nie spełnia warunków (np. `smugglers_thopter` nie zadziała bez 2+ wpływu u Gildii).
        
3. **Naprawiono błąd logiki `PAY` / `EXCHANGE`:**
    
    - **Problem:** Podobnie jak `CHOICE`, opcjonalne płatności (jak na karcie `Duncan Idaho`) były błędnie zdefiniowane w JSON i nie były wykrywane przez kod.
        
    - **Poprawka:** Poprawiliśmy funkcję `_find_decision_in_actions` (w `game_manager.py`), aby poprawnie wykrywała te efekty, co pozwala na uruchomienie okna decyzji.
        

### B. Błędy Fazy Odkrycia i Konfliktu

Te błędy powodowały, że Faza Odkrycia była niegrywalna i błędnie obliczała wyniki.

4. **Naprawiono krytyczny błąd `discard_pile`:**
    
    - **Problem:** Wejście w "Zarządzaj Ręką" (`set_player_hand` w `game_manager.py`) czyściło stos kart odrzuconych (`discard_pile`).
        
    - **Poprawka:** Usunęliśmy linię `player_state["discard_pile"] = []`. To naprawia całą logikę Fazy Odkrycia (np. efekty "Fremen Bond"), ponieważ gra teraz poprawnie "pamięta", co zagrałeś w Fazie Agentów.
        
5. **Naprawiono obliczanie siły (Swords) w konflikcie:**
    
    - **Problem:** Siła z wojsk (`troops_in_conflict * 2`) była błędnie dodawana już w momencie obliczania `calculate_reveal_stats`, zamiast w momencie rozstrzygania konfliktu.
        
    - **Poprawka:** Usunęliśmy te obliczenia z `calculate_reveal_stats` (w `game_manager.py`) i przenieśliśmy je do `resolve_conflict_auto` (w `app.py`). Teraz siła jest poprawnie sumowana z 3 źródeł (Karty + Intrygi + Wojsko) we właściwym momencie.
        
6. **Naprawiono obsługę efektów `PAY`/`CHOICE` w Fazie Odkrycia:**
    
    - **Problem:** Efekty takie jak `Gurney Halleck` ("zapłać 3 Solari...") lub `Bene Gesserit Sister` ("wybierz 2P lub 2S") były całkowicie ignorowane.
        
    - **Poprawka:** Zaktualizowaliśmy `calculate_reveal_stats` (w `game_manager.py`), aby czytała nowe, ustandaryzowane pola `possible actions`:
        
        - Dla `CHOICE` (jak `Bene Gesserit Sister`): Automatycznie wybiera Perswazję (najbardziej logiczną w tej fazie).
            
        - Dla `PAY` (jak `Gurney Halleck`): Dodaje do opisu karty w UI tag `[MANUAL ACTION]`, przypominając Ci o użyciu "Ręcznej Korekty".
            

### C. Standaryzacja Danych (JSON)

Te błędy były źródłem wielu problemów z logiką `CHOICE` i `PAY`.

7. **Ustandaryzowano `app/locations.json`:**
    
    - **Problem:** Plik używał błędnych kluczy (np. `gain1`, `exchange1`), co łamało parser.
        
    - **Poprawka:** Cały plik został zastąpiony wersją, która używa wyłącznie poprawnych list akcji (np. `actions: [ {"gain": ...}, {"gain": ...} ]`).
        
8. **Ustandaryzowano `app/cards.json`:**
    
    - **Problem:** Plik miał niespójne struktury `agent_effect` i chaotyczne `reveal_effect`.
        
    - **Poprawka:** Cały plik został zastąpiony wersją, która używa ustandaryzowanych, czystych list `actions` zarówno dla `agent_effect`, jak i `reveal_effect`.
        
9. **Ustandaryzowano `app/leaders.json`:**
    
    - **Problem:** Plik miał błędną strukturę `ability_signet.action`.
        
    - **Poprawka:** Cały plik został zastąpiony wersją, która używa poprawnej, płaskiej listy `action`.
        

### D. Nowe Funkcje i Usprawnienia

Na koniec, wdrożyliśmy nowe funkcje, o które prosiłeś, aby zwiększyć automatyzację i kontrolę.

10. **Wdrożono manualne dociąganie kart:**
    
    - **Problem:** Gra losowo dociągała karty, co odbierało Ci kontrolę (np. przy intrygach).
        
    - **Poprawka:** Usunęliśmy funkcję `draw_cards()`. Każdy efekt dociągnięcia karty (z lokacji, sygnetu, zdolności) generuje teraz wpis w historii: `MANUAL ACTION: Draw 1 card...`. Pozwala Ci to samemu wejść w "Zarządzaj Ręką" i wybrać, którą kartę chcesz dociągnąć.
        
11. **Wdrożono akumulację przyprawy:**
    
    - **Problem:** Nieużywane pola przyprawy nie stawały się bardziej atrakcyjne.
        
    - **Poprawka:** Pola `the_greate_flat`, `hagga_basin` i `imperial_basin` mają teraz licznik `bonus_spice` (w `game_stat.json`), który rośnie o +1 na koniec każdej rundy, jeśli nikt na nich nie stanął. Gracz, który tam wyląduje, zbiera cały bonus.
        
12. **Rozszerzono "Ręczną Korektę" (Manual Override):**
    
    - **Problem:** Korektor był zbyt prosty i nie pozwalał na edycję kluczowych elementów.
        
    - **Poprawka:** Dodaliśmy do panelu `manual_override.html` trzy nowe sekcje:
        
        1. Ręczne dodawanie/odejmowanie **Punktów Zwycięstwa (VP)**.
            
        2. Dodawanie dowolnej **Karty Intrygi** do ręki gracza.
            
        3. Ręczne ustawianie liczników **Bonusu Przyprawy** na lokacjach.