
###  Co to jest programowanie funkcyjne?

Wyobraź sobie, że piszesz instrukcję obsługi do jakiejś maszyny. Możesz opisać to na dwa sposoby:
- **Sposób 1 (imperatywny):** "Weź śrubokręt, odkręć śrubkę A, następnie podnieś klapkę B, a potem wciśnij przycisk C." To jest jak **programowanie imperatywne**
- **Sposób 2 (funkcyjny):** "Zapewnij, że klapka jest otwarta, a maszyna uruchomiona, aby uzyskać wynik." Tutaj opisujesz, **co** chcesz osiągnąć, a nie **jak** dokładnie to zrobić. Skupiasz się na **logice transformacji danych**.

---

### Co to jest programowanie funkcyjne (FP) w praktyce?

To **paradygmat programowania**, czyli pewien **sposób myślenia i podejścia do tworzenia oprogramowania**. W FP patrzymy na obliczenia jak na **ewaluację funkcji matematycznych**. Brzmi skomplikowanie? Wcale nie!

Myśl o tym tak: masz zestaw funkcji (jak w matematyce: f(x)=x2 albo g(x,y)=x+y). Te funkcje przyjmują jakieś dane wejściowe i zwracają wynik, ale co najważniejsze – **niczego nie zmieniają na zewnątrz**. Nie modyfikują żadnych globalnych zmiennych, nie zmieniają stanu systemu, po prostu obliczają i zwracają to, co mają zwrócić.

---

### Kluczowe cechy FP, które ułatwiają życie programistom:

- **Deklaratywność**: Zamiast mówić komputerowi _jak_ coś zrobić (np. "przejdź przez listę, dodaj do zmiennej `suma`"), mówimy mu _co_ chcemy osiągnąć (np. "oblicz sumę tej listy"). Kod staje się bardziej zwięzły i łatwiejszy do zrozumienia, bo odzwierciedla intencje, a nie szczegóły implementacji.
    
- **Brak efektów ubocznych**: Funkcje w programowaniu funkcyjnym są jak "czarne skrzynki". Wrzucasz do nich dane, dostajesz wynik, i nic więcej się nie dzieje. Nie wpływają na otoczenie, nie zmieniają danych poza swoim zakresem. Dzięki temu łatwiej przewidzieć, jak zachowa się program, bo jedna funkcja nie zepsuje czegoś, co robi inna.
    
- **Przewidywalność**: Skoro funkcje nie mają efektów ubocznych i zawsze zwracają ten sam wynik dla tych samych danych wejściowych, to zachowanie programu jest **dużo łatwiejsze do przewidzenia i debugowania**. Jeśli coś pójdzie nie tak, wiesz, że problem jest w samej funkcji, a nie w jakimś ukrytym stanie, który zmienił się gdzieś indziej.
    

> **💡 Analogia**: Wyobraź sobie kalkulator. Wrzucasz "2 + 2", dostajesz "4". Niezależnie od tego, ile razy to zrobisz, wynik zawsze będzie ten sam, a kalkulator nie zmieni swojej "temperatury" ani nie uszkodzi się od tego działania. To jest właśnie esencja czystej funkcji i myślenia funkcyjnego!

---

## Porównanie Paradygmatóws

### FP vs Imperatywne vs Obiektowe

|Aspekt|Funkcyjne|Imperatywne|Obiektowe|
|---|---|---|---|
|**Dane**|Niezmienne|Zmienne|Hermetyzowane|
|**Kontrola**|Funkcje|Sekwencja kroków|Metody obiektów|
|**Stan**|Unikany|Centralny|Enkapsulowany|


---

### Kiedy Czego Użyć?

- **Funkcyjne**: Przetwarzanie danych, transformacje, analiza.
- **Imperatywne**: Algorytmy krok-po-kroku, kontrola przepływu.
- **Obiektowe**: Modelowanie realnych systemów, duże aplikacje.

---

## Czyste Funkcje: Fundament FP

### Definicja

- Dla tych samych danych wejściowych **zawsze zwraca ten sam wynik**.
- **Nie powoduje żadnych efektów ubocznych**.

---

### Charakterystyka ✅

- **Determinizm**: Zawsze ten sam wynik.
- **Brak efektów ubocznych**: Bez modyfikacji danych globalnych.
- **Referencyjna przezroczystość**: Można zastąpić wywołanie funkcji jej wynikiem.

Python

```
# ✅ CZYSTA FUNKCJA
def square(x):
    return x * x

# ❌ NIECZYSTA FUNKCJA
counter = 0
def impure_increment():
    global counter
    counter += 1  # Modyfikuje stan globalny!
    return counter
```

---

### Zalety Czystych Funkcji

- **Łatwiejsze testowanie**: Brak ukrytych zależności.
- **Możliwość memoizacji**: Cache'owanie wyników.
- **Równoległość**: Bezpieczne w środowiskach wielowątkowych.
- **Kompozycja**: Łatwe łączenie.

> 🎯 **Przykład**: Kalkulator to czysta funkcja – 2+2 zawsze równa się 4.

---

## Niezmienność i Rekursja

### Niezmienność (Immutability)

Zamiast modyfikować istniejące dane, **tworzymy nowe struktury**.

Python

```
# ❌ Mutacja
original_list = [1, 2, 3]
original_list.append(4)  # Modyfikuje!

# ✅ Niezmienność
original_list = [1, 2, 3]
new_list = original_list + [4]  # Tworzy nową!
```

---

### Rekursja jako Alternatywa dla Pętli

**Wzorzec**:

1. **Przypadek bazowy** (warunek stopu).
2. **Wywołanie rekurencyjne** (funkcja wywołuje siebie z mniejszym problemem).

Python

```
def factorial(n):
    if n == 0:  # Przypadek bazowy
        return 1
    return n * factorial(n - 1) # Wywołanie rekurencyjne
```

---

### Kiedy Używać Rekursji?

- Struktury drzewiaste (katalogi, DOM).
- Problemy typu "podziel i zwyciężaj".
- Naturalne definicje matematyczne.

---

## Funkcje Wyższego Rzędu i Lambdy

### Funkcje Wyższego Rzędu (Higher-Order Functions)

Funkcje, które:

- Przyjmują inne funkcje jako argumenty.
- Zwracają funkcje.

Python

```
def apply_operation(numbers, operation):
    return [operation(num) for num in numbers]

def square(x): return x ** 2
numbers = [1, 2, 3, 4]
squared = apply_operation(numbers, square) # [1, 4, 9, 16]
```

---

### Lambdy (Funkcje Anonimowe)

Krótkie, jednolinijkowe funkcje dla prostych operacji.

Python

```
# Zamiast: def add_one(x): return x + 1
add_one = lambda x: x + 1

# Praktyczne użycie:
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, numbers)) # [1, 4, 9, 16, 25]
```

---

## Kluczowe Funkcje: `map()`, `filter()`, `reduce()`

### Wizualizacja Przepływu Danych

```
Dane wejściowe: [1, 2, 3, 4, 5]
        ↓
    map(x²)       → [1, 4, 9, 16, 25]
        ↓
    filter(>10)   → [16, 25]
        ↓
    reduce(sum)   → 41
```

---

### Implementacje i Przykłady

Python

```
from functools import reduce
data = [1, 2, 3, 4, 5]

# MAP: Transformacja każdego elementu
doubled = list(map(lambda x: x * 2, data)) # [2, 4, 6, 8, 10]

# FILTER: Selekcja elementów spełniających warunek
evens = list(filter(lambda x: x % 2 == 0, data)) # [2, 4]

# REDUCE: Agregacja do pojedynczej wartości
total = reduce(lambda acc, x: acc + x, data, 0) # 15
maximum = reduce(lambda acc, x: max(acc, x), data) # 5
```

---

### Praktyczne Zastosowania

- **`map()`**: Konwersja jednostek, formatowanie danych.
- **`filter()`**: Wyszukiwanie, walidacja danych.
- **`reduce()`**: Agregacje, statystyki, akumulatory.

---

## Kompozycja Funkcji

### Budowanie Złożoności z Prostych Elementów

**Matematycznie**: `(f ∘ g)(x) = f(g(x))`

Python

```
def double(x): return x * 2
def increment(x): return x + 1
def square(x): return x ** 2

# Ręczna kompozycja
result = double(increment(square(3))) # 3 -> 9 -> 10 -> 20

# Funkcja kompozycji (od prawej do lewej)
def compose(*functions):
    def inner(arg):
        result = arg
        for func in reversed(functions): result = func(result)
        return result
    return inner
transform = compose(double, increment, square)
result = transform(3) # 20
```

---

### Kompozycja Funkcji (Pipeline)

Python

```
# Pipeline (od lewej do prawej)
def pipeline(data, *functions):
    result = data
    for func in functions: result = func(result)
    return result

result = pipeline(3, square, increment, double) # 3 -> 9 -> 10 -> 20
```

---

### Korzyści Kompozycji

- **Modułowość**: Małe, testowalne funkcje.
- **Reużywalność**: Funkcje można łączyć na różne sposoby.
- **Czytelność**: Jasny przepływ transformacji danych.

---

## Zastosowania w Praktyce

### Data Science 📊

- **Pandas**: `df.filter().map().reduce()`
- **Apache Spark**: `rdd.map().filter().reduce()`

---

### Uczenie Maszynowe 🤖

- **TensorFlow/PyTorch**: Warstwy jako funkcje: `tensor -> tensor`.
    
    Python
    
    ```
    model = tf.keras.Sequential([
        tf.keras.layers.Dense(64, activation='relu'),
        tf.keras.layers.Dense(10, activation='softmax')
    ])
    ```
    

---

### Frontend Development 🌐

- **React**: Komponenty funkcjonalne, `filter().map()`
- **Redux**: Czyste reduktory – niezmienność!

---

### Przetwarzanie Strumieni 🌊

- Kafka Streams, Apache Flink, RxJS.
- Transformacje i agregacje w czasie rzeczywistym.

---

## Zalety i Wady

### ✅ Zalety

- **Jakość kodu**: Czytelność, łatwe testowanie i debugowanie.
- **Niezawodność**: Brak efektów ubocznych, niezmienność (brak race condition).
- **Wydajność**: Bezpieczna równoległość, memoizacja, optymalizacje kompilatora.

---

### ❌ Wady

- **Krzywa uczenia**: Zmiana sposobu myślenia, nowe koncepty.
- **Wydajność**: Więcej obiektów (pamięć, GC pressure), rekursja bez optymalizacji (stack overflow).
- **Praktyczność**: Niektóre algorytmy naturalnie imperatywne, trudna integracja z istniejącym kodem.

---

## Dobre Praktyki

### 🎯 Jak Zacząć?

1. **Małe kroki**: `map/filter/reduce` zamiast pętli.
2. **Czyste funkcje**: Unikaj globalnego stanu.
3. **Kompozycja nad dziedziczeniem**: Łącz funkcje.
4. **Immutability first**: Twórz nowe obiekty.

---

### 🛠️ Praktyczne Wskazówki

Python

```
# ✅ Dobrze - czysta funkcja
def calculate_tax(amount, rate): return amount * rate / 100

# ❌ Źle - efekt uboczny
tax_total = 0
def calculate_tax_bad(amount, rate):
    global tax_total
    tax = amount * rate / 100
    tax_total += tax # Efekt uboczny!
    return tax
```

---

### Praktyczne Wskazówki cd.

Python

```
# ✅ Dobrze - kompozycja funkcji
def process_order(order):
    return pipeline(
        order,
        validate_order,
        calculate_total,
        apply_discount,
        add_tax
    )

# ❌ Źle - długa funkcja z wieloma odpowiedzialnościami
def process_order_bad(order):
    # 50 linii kodu robiących wszystko...
    pass
```

---

## Następne Kroki

### 📚 Co Dalej?

- **Funkcyjne języki**: Haskell, Clojure, F#.
- **Biblioteki**: Ramda.js, toolz (Python), cats (Scala).
- **Wzorce**: Monady, funktory, aplikatywne funktory.
- **Projektowanie**: Event sourcing, CQRS.

---

### 🔧 Narzędzia do Eksperymentowania

- **Python**: `functools`, `itertools`, `operator`.
- **JavaScript**: Ramda, Lodash/FP, RxJS.
- **Online REPLs**: Repl.it, CodePen.

---

## Podsumowanie

### Programowanie Funkcyjne to potężny paradygmat, który:

- **Zwiększa jakość kodu** (czyste funkcje, niezmienność).
- **Ułatwia testowanie** (brak efektów ubocznych).
- **Wspiera równoległość** (bezpieczne współdzielenie danych).
- **Promuje kompozycję** zamiast dziedziczenia.

> **Pamiętaj**: Użyj podejścia funkcyjnego tam, gdzie przynosi korzyści!

---

## Pytania i Dyskusja

### Pytania do zastanowienia:

1. Jakie problemy w Twoich projektach mogłyby skorzystać z FP?
2. Gdzie widzisz największe wyzwania we wprowadzeniu funkcyjnych technik?
3. Które z przedstawionych konceptów wydają się najbardziej przydatne?