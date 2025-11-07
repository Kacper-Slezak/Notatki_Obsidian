### Cel projektu:
Kwantyfikacja i analiza zdolności Dużego Modelu Językowego (LLM, np. Gemini, GPT-4) do **efektywnej gry strategicznej** w wybranej grze planszowej. Ocenimy, w jakim stopniu LLM, bazując wyłącznie na instrukcjach tekstowych i historii rozgrywki, potrafi **utrzymać spójność strategiczną** i **poprawnie stosować złożone zasady** w warunkach długoterminowego planowania.

---
## Zakres

Projekt obejmie:

1. **Przeprowadzenie serii pełnych partii** _Diuny: Imperium_, gdzie LLM jest z jednym graczy.
    
2. **Analizę strategiczną LLM:** Ocenę jakości i spójności decyzji modelu w kontekście mechanik _deck-building_ i _worker placement_.
    
3. **Identyfikację błędów konwersacyjnych/kontekstowych:** Rejestrację przypadków, gdy LLM:
    
    - **Łamie zasady** (np. próbuje zagrać na zajęte pole lub użyć nieistniejącej karty).
        
    - **Zapomina o elementach gry** (np. o posiadanych zasobach, sojuszach).
        
    - **Wprowadza "halucynacje"** (np. błędnie opisuje stan planszy lub kartę).
        
4. **Testowanie Metody Promptowania (CoT):** Porównanie wyników i jakości ruchów, gdy poprosisz model, by **wyjaśnił swoją strategię** przed podjęciem decyzji.
    

---

## Plan Działania

1. **Wybór i Konfiguracja Modelu:** Wybór konkretnego modelu LLM do testów (np. Gemini, GPT-4) i ustalenie optymalnego wstępnego "promptu" inicjującego rozgrywkę (wstępny opis zasad i celów gry).
    
2. **Opracowanie Protokołu Dialogu:** Stworzenie **standardowego szablonu tekstowego**, którego będziesz używać do opisywania LLM-owi stanu gry po każdym ruchu (Twoim i jego), zapewniając spójność danych wejściowych.
    
3. **Faza Eksperymentów Interaktywnych:**
    
    - **Rozgrywka Wstępna (Baseline):** Rozegranie serii partii  bez dodatkowych instrukcji analitycznych dla modelu.
        
    - **Rozgrywka z CoT:** Rozegranie kolejnej serii partii, instruując LLM, aby **zawsze** najpierw **wytłumaczył powód ruchu**, a dopiero potem podał ruch.
        
4. **Zbiór Danych i Analiza:**
    
    - Rejestrowanie każdego ruchu, błędów i ewentualnych wyjaśnień LLM.
        
    - Końcowa ocena strategiczna: Porównanie Twojego wyniku/wskaźnika zwycięstw (jako doświadczonego gracza) z wynikiem LLM.
        
5. **Wnioski:** Ustalenie, w których obszarach (Worker Placement, Deck-Building, Konflikt) LLM radzi sobie najlepiej, a gdzie **rozpada się jego zdolność do utrzymania kontekstu strategicznego**.