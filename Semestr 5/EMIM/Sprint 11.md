
# Raport z Podsumowania Sprintu 11:  Analiza Strategiczna i Taktyczna

Projekt: Mistrz Gry
## 1. Cel Sprintu

Głównym celem tego etapu była rygorystyczna ocena jakościowa (jak _dobrze_ AI gra).

Zgodnie z założeniami, skupiliśmy się na **niezależnej analizie systematycznej**. Aby wyeliminować subiektywizm pojedynczego obserwatora, zapisy poszczególnych partii zostały poddane ocenie przez nas, którzy niezależnie od siebie punktowali każdy ruch AI w dwóch wymiarach:

- **Ocena Taktyczna (Short-term):** Czy ruch był optymalny w kontekście bieżącej tury?
    
- **Ocena Strategiczna (Long-term):** Czy ruch przybliżał do zwycięstwa w perspektywie całej gry?
    

## 2. Metodologia Oceny

Do analizy wykorzystano zapisy z rozegranych partii (w tym partii z modyfikacjami i losowym startem).

Punkty przyznawane były w skali 1-5:

- **Skala 1:** Ruch krytycznie błędny, szkodliwy dla gracza.
    
- **Skala 3:** Ruch poprawny, standardowy, "nijaki".
    
- **Skala 5:** Ruch wybitny, optymalny, wykorzystujący pełen potencjał sytuacji.
    
## 3. Wyniki Analizy Danych

### A. Dysproporcja Taktyczno-Strategiczna

Zauważalny jest stały trend, gdzie oceny taktyczne są wyższe niż strategiczne (np. ruchy oceniane Taktyka: 4 / Strategia: 2).

- **Wniosek:** AI świetnie radzi sobie z "księgowością" gry. Jeśli celem jest maksymalizacja zasobów w danej turze, model robi to dobrze. Jednakże często te "dobre" ruchy nie przekładają się na realizację nadrzędnego celu (Zwycięstwa). Model potrafi wygrać bitwę o zasoby, przegrywając wojnę o punkty (VP).

### B. Błędy w Deck-Buildingu (Zarządzanie Talią)

- **Syndrom "Arrakis Liaison":** AI ma tendencję do kupowania tanich kart "zapychaczy", rozwadniając swoją talię. Nie rozumie, że niekupienie niczego jest czasem lepsze niż kupienie słabej karty.
    
- **Czyszczenie Talii:** Model często niszczy niewłaściwe karty lub robi to w momentach, gdy nie przynosi to korzyści strategicznej.
    
### C. Zarządzanie Konfliktem i Zasobami

Dane pokazują skrajności w zachowaniu militarnym.

- **Overkill lub Pasywność:** AI ma problem z wyczuciem "progu opłacalności" w konflikcie. Zdarzało mu się wysyłać zbyt duże siły do walki o niską stawkę lub całkowicie ignorować konflikt, gdy tanim kosztem mogło zdobyć 2. miejsce.
    
- **Chomikowanie (Hoarding):**  AI zbiera zasoby dla samego zbierania, często kończąc grę z fortuną, której nie zdążyło zamienić na punkty zwycięstwa.
    
### D. Zgodność Ocen

Porównanie ocen pokazało wysoką zgodność w ocenie ruchów skrajnych (bardzo dobrych i bardzo złych). Rozbieżności pojawiały się przy ruchach "przeciętnych", gdzie jedena osoba widziała w nich przygotowanie pod przyszły ruch, a inny stratę tempa. 
## 4. Podsumowanie Projektu i Wnioski Końcowe

Projekt **Mistrz Gry** wykazał, że Duże Modele Językowesą w stanie uczestniczyć w złożonej grze planszowej z niepełną informacją, ale z wyraźnymi ograniczeniami:

1. **Poziom Kompetencji:** AI osiągnęło poziom **"Zaawansowanego Nowicjusza"**. Potrafi grać zgodnie z zasadami, nie wykonuje ruchów nielegalnych (dzięki walidacji interfejsu) i potrafi optymalizować proste łańcuchy ekonomiczne.
    
2. **Bariera Abstrakcji:** AI nie posiada "instynktu gracza". Nie potrafi blefować, nie rozumie psychologii stołu (np. "przeciwnik na pewno tam nie pójdzie, bo to mu się nie opłaca") i ma trudności z adaptacją strategii w momencie, gdy pierwotny plan zostaje zablokowany.
    
3. **Wnioski dla Prompt Engineeringu:** Kluczem do sukcesu nie jest inteligencja modelu, ale **kontekst**. Najlepsze wyniki osiągaliśmy, gdy "karmiliśmy" AI nie tylko stanem planszy, ale też jego własną "pamięcią" (Notatki Strategiczne) i narzuconymi heurystykami (np. w późnej fazie gry: "Ignoruj ekonomię, kupuj VP").