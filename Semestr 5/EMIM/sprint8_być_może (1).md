Oto raport zredagowany w bardziej naturalnym, "ludzkim" tonie, typowym dla podsumowania prac zespołu projektowego/deweloperskiego.

---

# Raport z Podsumowania Sprintu 8: Pamięć Strategiczna i testy na żywym organizmie

Projekt: Mistrz Gry

Model: GPT-3 Pro (Nowy model "Myślący")

## 1. Co robiliśmy w tym sprincie?

Po problemach z "amnezją" AI, które zdiagnozowaliśmy w Sprincie 7, w tym tygodniu mieliśmy jeden główny cel: **sprawić, żeby AI pamiętało, co chciało zrobić turę wcześniej**.

Wdrożyliśmy rozwiązanie oparte na **"Notatce Strategicznej" (Grand Strategy)**. AI na początku gry ustala plan, a potem co rundę go aktualizuje i dostaje go z powrotem w każdym kolejnym prompcie. Przy okazji przetestowaliśmy, jak w naszym interfejsie poradzi sobie nowszy model językowy (GPT-3 Pro).

## 2. Jak zadziałała "Pamięć"?

Mechanizm zadziałał świetnie. Problem chaotycznych, losowych decyzji zniknął. AI konsekwentnie realizowało cele długoterminowe – np. uparło się na zdobycie _Swordmastera_ i faktycznie uzbierało na niego fundusze, zamiast wydawać je na nie potrzebne akcje.

## 3. Nowy model: Dobry gracz z problemami

Przesiadka na GPT-3 Pro to była duża zmiana, która ma swoje plusy i minusy:

- **Plusy:** Do połowy gry (ok. 5 rundy) AI grało bezbłędnie. Poziom dobrego gracza. Optymalnie zarządzało ekonomią i zrealizowało plan szybkiego wejścia do Wysokiej Rady (High Council).

- **Minusy ("Sztywność"):** Ten model jest bardzo literalny. Poprzednie wersje potrafiły się "domyślić" o co chodzi, jeśli w danych była literówka. Ten model, gdy widzi błąd w JSON-ie, odmawia współpracy lub się zacina. To utrudniało nam ręczne poprawki w trakcie gry.

- **Końcówka:** W rundach 7-9 model zaczął się gubić. Przez nadmiar danych  zaczął halucynować – próbował zagrywać karty, których nie miał, albo wchodzić na zablokowane pola (np. akcja z _Foldspace_). Nie spotkaliśmy się z tym w takiej ilości używajac poprzedniego modelu. 

## 4. AI  vs Człowiek – Dlaczego przegraliśmy?

Mieliśmy świetną okazję, żeby porównać "myśli" AI z zapiskami Nowicjusza. To zestawienie pokazuje, dlaczego mimo świetnej ekonomii, AI przegrało.

1. **Syndrom "Eurogry" vs Wyścig:**
    
    - **AI:** Grało jak w grę ekonomiczną. Cieszyło się, że ma dużo surowców i "efektywną talię". Nawet w ostatnich rundach marnowało akcje na czyszczenie talii (_Fedaykin Death Commando_), zamiast zbierać punkty zwycięstwa.
    
    - **Nowicjusz:** Od początku traktowała to jak wyścig. Jej notatki to ciągłe: _"Muszę zdobyć punkt"_, _"Jedyna nadzieja to wygrana bitwa"_. To proste nastawienie na cel okazało się lepsze niż skomplikowana optymalizacja silnika przez AI.
    
2. **Elastyczność:**
    
    - Kiedy AI zablokowało Martynie pole agenta, ona natychmiast zmieniła plan i kupiła _Wysoką Radę_. AI, gdy napotykało przeszkodę, często próbowało forsować pierwotny plan, co przy błędach w danych prowadziło do paraliżu decyzyjnego.
    
3. **Brak "Instynktu Zabójcy" (Kluczowy błąd):**
    
    - W 8. rundzie AI miało wojsko i mogło walczyć o cenne 2. miejsce w konflikcie. Zamiast tego zagrało kartę intrygi _Wycofanie (Retreat)_ i oddało pole bez walki. Model uznał, że skoro nie wygra 1. miejsca, to nie opłaca się walczyć wcale. To była fatalna decyzja, która kosztowała go grę. AI było "bogate, ale martwe" – skończyło z nadmiarem przyprawy, której nie zdążyło wydać.
4. **Wyniki**:
	 - Choć nowicjusz nie wygrał gry, którą wygrał bardziej doświadczony gracz to zdobył drugie miejsce z przewagą dwóch punktów zwycięstwa nad AI (w skali do 10-12)

## 5. Wnioski na przyszłość

Sama inteligencja modelu i "pamięć" to za mało. AI brakuje instynktu gracza turniejowego. Musimy mu go zaprogramować.

1. **Musimy wymusić agresję:** AI nie rozumie, że w końcówce gry optymalizacja nie ma znaczenia.

2. **Dane muszą być idealne:** Nowy model nie wybacza błędów w stanie gry. Musimy poprawić tak by nie poprawiać wysłanego prompta.

3. **Halucynacje:** Model zaczyna halucynować i odbiegać od poziomu poprzedniej gry w końcowych rundach, musimy spróbować to poprawić 

## 6. Plan na Sprint 9

1. **Wdrożenie "Wskazówek Fazowych":** Będziemy doklejać do promptu instrukcje dla końcowych etapów gry (np. _"Runda 8: To koniec gry. Atakuj! Nie oszczędzaj zasobów, kupuj tylko punkty"_). To propozycja (Opcja E) z poprzedniego raportu, która teraz wydaje się niezbędna.

2. **Czyszczenie danych:** Poprawki w generatorze promptów, żeby wyeliminować błędy, na których wykłada się nowy model.

3. **Test**: Kolejny test gry z AI gdyż jedna rozgrywka nie definiuje jego regularnego zachowania oraz nie dostarcza wystarczająco danych 