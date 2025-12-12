	### Problem 1: Błąd w logice "Warunków" Fazy Odkrycia (np. `Firm Grip`)

Gdy naprawialiśmy `calculate_reveal_stats` (Poprawka 11), wprowadziliśmy logikę, która sprawdza warunki. Np. dla `Sietch Reverend Mother` sprawdzamy, czy w `discard_pile` jest karta Fremenów.

**Gdzie jest błąd:** W przypadku karty `Firm Grip` (która daje +4 Perswazji za sojusz z Imperatorem), nasza logika w `calculate_reveal_stats` sprawdza to w uproszczony sposób: `has_emperor_alliance = player_influence.get("emperor", 0) >= 4`.

To jest **błędne założenie**. W Dune: Imperium sojusz ma się wtedy, gdy ma się _więcej_ wpływu niż ktokolwiek inny _i_ co najmniej 4. Możesz mieć 5 wpływu, ale jeśli przeciwnik ma 6, to _nie masz_ sojuszu (i `Firm Grip` nie powinien zadziałać).

Prawidłowe sprawdzenie sojuszu musi odwołać się do globalnego stanu `game_state.alliances`.

**Rezultat:** `Firm Grip` (i podobne karty) będą dawać bonusy niepoprawnie, bazując tylko na wpływie gracza, a nie na tym, czy faktycznie posiada on token sojuszu.

---

### Problem 2: Niezastosowane pasywne zdolności Liderów (np. `Countess Ariana`)

Zaimplementowaliśmy zdolności liderów, które aktywują się przy _ruchu_ (np. `Duke Leto` – tańsze pola, `Count Ilban` – dociąg karty), ale zignorowaliśmy zdolności, które modyfikują _zyski_.

**Gdzie jest błąd:** Weźmy `Countess Ariana Thorvald`. Jej zdolność pasywna to: "When you gather spice, you get 1 Spice less and draw a card from unplayed pile."

Nasza funkcja `_apply_gain` (w `game_manager.py`), która jest sercem wszystkich zysków w grze, w ogóle nie sprawdza, _kim jest_ gracz otrzymujący zasoby. Kiedy `_apply_gain` daje komuś "Spice", po prostu je dodaje, ignorując zdolność Ariany.

**Rezultat:** Pasywne zdolności liderów, które modyfikują zyski (jak `Countess Ariana`), są całkowicie pominięte w logice gry, co psuje balans tych postaci.

---

### Problem 3: Błędne dane dla AI (Problem z `build_ai_prompt.py`)

Ten błąd jest subtelny, ale kluczowy dla automatyzacji AI.

**Gdzie jest błąd:** Skrypt `build_ai_prompt.py`, gdy generuje prompt dla Fazy Odkrycia (Reveal), pobiera dane o sile i perswazji graczy (w tym AI) z `game_state.json` (z klucza `reveal_stats`).

Jednak nasza nowa, inteligentna funkcja `calculate_reveal_stats` (którą wdrożyliśmy w Poprawce 11) wykonuje skomplikowane obliczenia "w locie" (np. automatycznie wybiera Perswazję dla `Bene Gesserit Sister` i sprawdza `Fremen Bond`).

`build_ai_prompt.py` **nie wywołuje** tej nowej funkcji. Czyta stare, "głupie" dane ze stanu gry.

**Rezultat:** AI (`Peter`) otrzymuje błędne informacje o swojej sile i (co ważniejsze) o swojej sile nabywczej (Perswazji). AI nie będzie wiedziało, że `Bene Gesserit Sister` dała mu +2 Perswazji, ani nie będzie świadome, że `Gurney Halleck` ma opcję `[MANUAL ACTION]`. Prompt dla AI jest niekompletny.

---

### Problem 4: Niewykorzystany potencjał Korektora (Manual Override)

W Poprawce 12 bardzo rozbudowaliśmy Korektor. Dodaliśmy VP, Intrygi i Bonus Przyprawy.

**Gdzie jest błąd (a raczej brak):** Nadal brakuje mu jednej, kluczowej funkcji, o którą pierwotnie prosiłeś: **możliwości edycji kart gracza**.

Obecnie mamy `manage_hand`, ale jest to narzędzie "wszystko albo nic" – ustawia całą rękę od nowa i resetuje `draw_deck`. Jest bezużyteczne, jeśli chcesz po prostu _przenieść jedną kartę_ z `discard_pile` do `draw_deck` (np. po pomyłce) albo _usunąć_ jedną kartę z ręki gracza (np. po efekcie `Test of Humanity`, który zmusza do odrzucenia karty).

**Rezultat:** Korektor nadal nie jest kompletnym narzędziem do "naprawiania" stanu gry, jeśli błąd dotyczy talii gracza. Brakuje mu "chirurgicznej precyzji".

---

### Podsumowanie nowych błędów

Mamy więc 4 nowe, duże obszary do poprawy:

1. **Błąd logiki `calculate_reveal_stats`** (błędne sprawdzanie sojuszu zamiast `influence >= 4`).
    
2. **Brakująca logika Pasywnych Liderów** (np. `Countess Ariana` nie działa, gdy `_apply_gain` daje przyprawę).
    
3. **Błędny Prompt AI** (`build_ai_prompt.py` nie używa nowej, inteligentnej funkcji `calculate_reveal_stats`).
    
4. **Niewykorzystany potencjał Korektora** (brak możliwości precyzyjnej edycji `hand`, `discard_pile`, `deck_pool`).
    

Daj znać, od którego problemu chcesz zacząć. Sugeruję zacząć od **Problemu 1**, ponieważ jest to ewidentny błąd logiczny w funkcji, którą niedawno modyfikowaliśmy.