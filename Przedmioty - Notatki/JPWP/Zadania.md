

---

## Zadanie 1: Prosty Kalkulator z Funkcjami Wyższego Rzędu

### Kod Zadania (do uzupełnienia)

```python
import math
from typing import Callable, Optional

# Zadanie 1: Prosty Kalkulator z Funkcjami Wyższego Rzędu
# Cel: Stwórz kalkulator, który używa funkcji wyższego rzędu do definiowania operacji matematycznych.
# Zamiast czterech oddzielnych funkcji, będziemy mieli jedną funkcję 'calculate',
# która przyjmuje operację (inną funkcję) jako argument.
# Dodatkowo, obsłuż dzielenie przez zero, zwracając 'None' dla wskazania błędu.

class FunctionalCalculator:
    ZERO = 0.0

    def calculate(self, a: float, b: float, operation: Callable[[float, float], float]) -> float:
        """
        Wykonuje operację matematyczną na dwóch liczbach.
        :param a: Pierwsza liczba.
        :param b: Druga liczba.
        :param operation: Funkcja (callable), która definiuje operację (np. dodawanie, odejmowanie).
        :return: Wynik operacji.
        """
        # TODO 1: Zaimplementuj logikę wykonania operacji.
        pass

    def calculate_safe(self, a: float, b: float, operation: Callable[[float, float], Optional[float]]) -> Optional[float]:
        """
        Wykonuje operację matematyczną na dwóch liczbach, zwracając Optional[float]
        w celu bezpiecznej obsługi potencjalnych błędów (np. dzielenia przez zero).
        :param a: Pierwsza liczba.
        :param b: Druga liczba.
        :param operation: Funkcja (callable), która definiuje operację i zwraca Optional[float].
        :return: Wynik operacji lub None, jeśli wystąpił błąd.
        """
        # TODO 2: Zaimplementuj logikę bezpiecznego wykonania operacji.
        pass

if __name__ == "__main__":
    calculator = FunctionalCalculator()

    # TODO 3: Zdefiniuj operacje dodawania, odejmowania i mnożenia jako funkcje lambda.
    add = None
    subtract = None
    multiply = None

    # TODO 4: Zdefiniuj funkcję dzielenia 'divide_safe', która zwraca None w przypadku dzielenia przez zero.
    def divide_safe(x: float, y: float) -> Optional[float]:
        pass

    # Przykładowe użycie (po uzupełnieniu TODOs)
    # print(f"Dodawanie (5 + 3): {calculator.calculate(5, 3, add)}")
    # print(f"Dzielenie (10 / 2) bezpiecznie: {calculator.calculate_safe(10, 2, divide_safe)}")
    # print(f"Dzielenie (5 / 0) bezpiecznie: {calculator.calculate_safe(5, 0, divide_safe)}")
```

### Kod Rozwiązania

```python
import math
from typing import Callable, Optional

class FunctionalCalculator:
    ZERO = 0.0

    def calculate(self, a: float, b: float, operation: Callable[[float, float], float]) -> float:
        """
        Wykonuje operację matematyczną na dwóch liczbach.
        :param a: Pierwsza liczba.
        :param b: Druga liczba.
        :param operation: Funkcja (callable), która definiuje operację (np. dodawanie, odejmowanie).
        :return: Wynik operacji.
        """
        return operation(a, b)

    def calculate_safe(self, a: float, b: float, operation: Callable[[float, float], Optional[float]]) -> Optional[float]:
        """
        Wykonuje operację matematyczną na dwóch liczbach, zwracając Optional[float]
        w celu bezpiecznej obsługi potencjalnych błędów (np. dzielenia przez zero).
        :param a: Pierwsza liczba.
        :param b: Druga liczba.
        :param operation: Funkcja (callable), która definiuje operację i zwraca Optional[float].
        :return: Wynik operacji lub None, jeśli wystąpił błąd.
        """
        return operation(a, b)

if __name__ == "__main__":
    calculator = FunctionalCalculator()

    # Zdefiniowane operacje
    add = lambda x, y: x + y
    subtract = lambda x, y: x - y
    multiply = lambda x, y: x * y

    # Funkcja dzielenia zwracająca Optional[float]
    def divide_safe(x: float, y: float) -> Optional[float]:
        if y == FunctionalCalculator.ZERO:
            return None # Zwraca None w przypadku błędu
        return x / y

    # --- Użycie kalkulatora ---
    print("--- Zwykłe obliczenia ---")
    print(f"Dodawanie (5 + 3): {calculator.calculate(5, 3, add)}")
    print(f"Odejmowanie (10 - 4): {calculator.calculate(10, 4, subtract)}")
    print(f"Mnożenie (2 * 6): {calculator.calculate(2, 6, multiply)}")

    print("\n--- Bezpieczne obliczenia (z Optional) ---")
    result_safe_divide = calculator.calculate_safe(10, 2, divide_safe)
    print(f"Dzielenie (10 / 2) bezpiecznie: {result_safe_divide if result_safe_divide is not None else 'Błąd'}")

    result_safe_divide_by_zero = calculator.calculate_safe(5, 0, divide_safe)
    print(f"Dzielenie (5 / 0) bezpiecznie: {result_safe_divide_by_zero if result_safe_divide_by_zero is not None else 'Błąd: Dzielenie przez zero!'}")
```

---

## Zadanie 2: Analiza Statystyk Listy Liczb (Funkcyjne Podejście)

### Kod Zadania (do uzupełnienia)

```python
from functools import reduce
from typing import Dict, Optional, List

# Zadanie 2: Analiza Statystyk Listy Liczb (Funkcyjne Podejście)
# Cel: Zoptymalizuj kod do analizy listy liczb (min, max, średnia, suma),
# wykorzystując funkcję 'reduce' do wykonania wszystkich obliczeń w jednym przejściu.
# Odpowiedz na pytania w komentarzach.

def analyze_numbers_functional_single_pass(numbers: List[int]) -> Dict[str, Optional[float]]:
    """
    Analizuje listę liczb i zwraca statystyki (min, max, suma, średnia)
    wykorzystując funkcyjne podejście i pojedyncze przejście z reduce.
    """
    if not numbers:
        return {"min": None, "max": None, "sum": 0, "average": None}

    # TODO 1: Jakie korzyści płyną z pojedynczego przejścia po liście w porównaniu do wielu pętli?
    # Odpowiedź 1:

    # TODO 2: Zaimplementuj funkcję redukującą (akumulator), która będzie zbierać min, max, sumę i count.
    # Ta funkcja powinna przyjmować bieżący stan (słownik) i nową liczbę, zwracając nowy stan.
    def stats_accumulator(acc: Dict[str, float], x: int) -> Dict[str, float]:
        pass

    # TODO 3: Zdefiniuj początkową wartość akumulatora (initial_stats) dla funkcji reduce.
    # Pamiętaj o obsłudze przypadku, gdy 'numbers' nie jest pusta.
    initial_stats = None

    # TODO 4: Użyj 'reduce' z zaimplementowanym akumulatorem i wartością początkową.
    final_stats = None

    # TODO 5: Wyciągnij końcowe wartości statystyk i oblicz średnią, pamiętając o przypadku dzielenia przez zero.
    min_value = None
    max_value = None
    total_sum = None
    average_value = None

    return {
        "min": float(min_value) if min_value is not None else None,
        "max": float(max_value) if max_value is not None else None,
        "sum": float(total_sum),
        "average": average_value
    }

if __name__ == "__main__":
    numbers_list = [3, 7, 2, 9, 4, 10, 5]
    # stats = analyze_numbers_functional_single_pass(numbers_list)
    # print(f"Maksymalna wartość: {stats['max']}")
```

### Kod Rozwiązania

```python
from functools import reduce
from typing import Dict, Optional, List

class FunctionalCalculator:
    ZERO = 0.0

def analyze_numbers_functional_single_pass(numbers: List[int]) -> Dict[str, Optional[float]]:
    """
    Analizuje listę liczb i zwraca statystyki (min, max, suma, średnia)
    wykorzystując funkcyjne podejście i pojedyncze przejście z reduce.
    """
    if not numbers:
        return {"min": None, "max": None, "sum": 0, "average": None}

    # Odpowiedź 1: Zwiększona wydajność (szczególnie dla dużych list),
    # mniejsze zużycie zasobów (mniej iteracji), elegancja i zwięzłość kodu,
    # lepsze odzwierciedlenie "funkcyjnej" idei agregacji.

    # Akumulator dla reduce, który zbiera wszystkie statystyki w jednym przebiegu
    def stats_accumulator(acc: Dict[str, float], x: int) -> Dict[str, float]:
        # Zawsze zwracamy NOWY słownik, aby zachować niezmienność
        return {
            'min': min(acc['min'], x),
            'max': max(acc['max'], x),
            'sum': acc['sum'] + x,
            'count': acc['count'] + 1
        }

    # Początkowe statystyki dla reduce. Używamy nieskończoności dla min/max,
    # aby pierwsza wartość z listy je poprawnie zainicjowała.
    initial_stats = {'min': float('inf'), 'max': float('-inf'), 'sum': 0.0, 'count': 0.0}

    final_stats = reduce(stats_accumulator, numbers, initial_stats)

    # Wyciągamy i obliczamy końcowe statystyki
    min_value = final_stats['min'] if final_stats['count'] > 0 else None
    max_value = final_stats['max'] if final_stats['count'] > 0 else None
    total_sum = final_stats['sum']
    average_value = total_sum / final_stats['count'] if final_stats['count'] > 0 else None

    return {
        "min": float(min_value) if min_value is not None else None,
        "max": float(max_value) if max_value is not None else None,
        "sum": float(total_sum),
        "average": average_value
    }

if __name__ == "__main__":
    numbers_list = [3, 7, 2, 9, 4, 10, 5]
    stats = analyze_numbers_functional_single_pass(numbers_list)

    print(f"Maksymalna wartość: {stats['max']}")
    print(f"Minimalna wartość: {stats['min']}")
    print(f"Suma wartości: {stats['sum']}")
    print(f"Średnia wartość: {stats['average']}")

    empty_list_stats = analyze_numbers_functional_single_pass([])
    print(f"\nStatystyki dla pustej listy: {empty_list_stats}")
```

---

## Zadanie 3: Filtrowanie i Mapowanie Listy Obiektów

### Kod Zadania (do uzupełnienia)

```python
from typing import Callable, List

# Zadanie 3: Filtrowanie i Mapowanie Listy Obiektów
# Cel: Mając listę obiektów 'Product', filtruj te, które spełniają warunek,
# a następnie przekształć je w inną formę, używając 'list comprehensions'.
# Zadbaj o niezmienność. Dodatkowo, wprowadź funkcję do tworzenia dynamicznych filtrów.

class Product:
    def __init__(self, name: str, price: float, in_stock: bool):
        self.name = name
        self.price = price
        self.in_stock = in_stock

    def __repr__(self):
        return f"Product(name='{self.name}', price={self.price}, in_stock={self.in_stock})"

def process_products(products: List[Product]) -> List[str]:
    """
    Filtruje produkty i zwraca listę ich nazw w formacie "Nazwa (Cena zł)"
    dla produktów dostępnych i droższych niż 50.
    """
    # TODO 1: Użyj list comprehension do przefiltrowania produktów,
    # które są "in_stock" (dostępne) ORAZ ich cena jest wyższa niż 50.0.
    # Następnie przekształć je w stringi w formacie "Nazwa (Cena zł)".
    # Wynik powinien być nową listą, nie modyfikując oryginalnej (zasada niezmienności).
    filtered_and_mapped_products = []
    return filtered_and_mapped_products

# TODO 2: Zaimplementuj funkcję 'create_price_filter', która przyjmuje minimalną cenę
# i zwraca inną funkcję, która będzie filtrować produkty na podstawie tej ceny.
def create_price_filter(min_price: float) -> Callable[[Product], bool]:
    pass

if __name__ == "__main__":
    products_list = [
        Product("Laptop", 1200.0, True),
        Product("Myszka", 25.0, True),
        Product("Klawiatura", 75.0, False),
        Product("Monitor", 300.0, True),
        Product("Kamera", 50.0, False),
        Product("Słuchawki", 120.0, True)
    ]

    # TODO 3: Wywołaj 'process_products' i wydrukuj wyniki.
    # processed_names = process_products(products_list)
    # print("Dostępne produkty (powyżej 50 zł):")

    # TODO 4: Użyj 'create_price_filter' do stworzenia dynamicznych filtrów
    # i zastosuj je do listy produktów.
    # filter_above_100 = create_price_filter(100.0)
    # high_value_products = [p for p in products_list if p.in_stock and filter_above_100(p)]
    # print(f"Produkty dostępne i droższe niż 100 zł: {high_value_products}")
```

### Kod Rozwiązania

```python
from typing import Callable, List

class Product:
    def __init__(self, name: str, price: float, in_stock: bool):
        self.name = name
        self.price = price
        self.in_stock = in_stock

    def __repr__(self):
        return f"Product(name='{self.name}', price={self.price}, in_stock={self.in_stock})"

def process_products(products: List[Product]) -> List[str]:
    """
    Filtruje produkty i zwraca listę ich nazw w formacie "Nazwa (Cena zł)"
    dla produktów dostępnych i droższych niż 50.
    """
    filtered_and_mapped_products = [
        f"{p.name} ({p.price:.2f} zł)"
        for p in products
        if p.in_stock and p.price > 50.0
    ]
    return filtered_and_mapped_products

def create_price_filter(min_price: float) -> Callable[[Product], bool]:
    """
    Zwraca funkcję filtrującą produkty na podstawie minimalnej ceny.
    Jest to przykład 'częściowego stosowania' (partial application), gdzie funkcja
    zwraca inną funkcję, która "pamięta" wartość 'min_price'.
    """
    return lambda product: product.price > min_price

if __name__ == "__main__":
    products_list = [
        Product("Laptop", 1200.0, True),
        Product("Myszka", 25.0, True),
        Product("Klawiatura", 75.0, False),
        Product("Monitor", 300.0, True),
        Product("Kamera", 50.0, False),
        Product("Słuchawki", 120.0, True)
    ]

    processed_names = process_products(products_list)
    print("Dostępne produkty (powyżej 50 zł):")
    for name in processed_names:
        print(f"- {name}")

    print(f"\nOryginalna lista produktów pozostała niezmieniona: {products_list}")

    print("\n--- Użycie dynamicznego filtra cenowego (częściowe stosowanie) ---")
    filter_above_100 = create_price_filter(100.0)
    high_value_products = [p for p in products_list if p.in_stock and filter_above_100(p)]
    print(f"Produkty dostępne i droższe niż 100 zł: {high_value_products}")

    filter_above_200 = create_price_filter(200.0)
    very_high_value_products = [p for p in products_list if p.in_stock and filter_above_200(p)]
    print(f"Produkty dostępne i droższe niż 200 zł: {very_high_value_products}")
```

---

## Zadanie 4: Kompozycja Funkcji do Przetwarzania Danych

### Kod Zadania (do uzupełnienia)

```python
from typing import Callable, List, Any

# Zadanie 4: Kompozycja Funkcji do Przetwarzania Danych
# Cel: Zaimplementuj funkcję 'compose', która przyjmuje wiele funkcji i zwraca jedną, złożoną funkcję,
# która je wywołuje w odpowiedniej kolejności (od prawej do lewej).
# Następnie zaimplementuj 'pipeline' dla kolejności od lewej do prawej.
# Użyj tych funkcji do przetworzenia listy danych.

def compose(*functions: Callable[[Any], Any]) -> Callable[[Any], Any]:
    """
    Tworzy złożoną funkcję, która wykonuje podane funkcje w kolejności
    od prawej do lewej (jak w matematyce: f(g(x))).
    :param functions: Funkcje do skomponowania.
    :return: Skomponowana funkcja.
    """
    # TODO 1: Zaimplementuj logikę kompozycji funkcji.
    pass

def pipeline(*functions: Callable[[Any], Any]) -> Callable[[Any], Any]:
    """
    Tworzy złożoną funkcję (pipeline), która wykonuje podane funkcje w kolejności
    od lewej do prawej.
    :param functions: Funkcje do skomponowania.
    :return: Skomponowana funkcja.
    """
    # TODO 2: Zaimplementuj logikę pipeline'u funkcji.
    pass

if __name__ == "__main__":
    # Przykładowe funkcje do kompozycji
    def add_five(x: int) -> int: return x + 5
    def multiply_by_two(x: int) -> int: return x * 2
    def to_string(x: int) -> str: return str(x) + "!"
    def capitalize_string(s: str) -> str: return s.upper()

    print("--- Kompozycja funkcji (f(g(x))) ---")
    # TODO 3: Użyj 'compose' do stworzenia funkcji, która najpierw doda 5,
    # potem pomnoży przez 2, potem zamieni na string, a na końcu zamieni na duże litery.
    # Pamiętaj o kolejności (od prawej do lewej dla compose).
    # transform_data_composed = compose(...)
    # print(f"Wynik compose dla 3: {transform_data_composed(3)}")

    print("\n--- Pipeline funkcji (f | g | h) ---")
    # TODO 4: Użyj 'pipeline' do stworzenia funkcji, która najpierw doda 5,
    # potem pomnoży przez 2, potem zamieni na string, a na końcu zamieni na duże litery.
    # Pamiętaj o kolejności (od lewej do prawej dla pipeline).
    # transform_data_pipeline = pipeline(...)
    # print(f"Wynik pipeline dla 3: {transform_data_pipeline(3)}")

    # TODO 5: Zastosuj jedną ze skomponowanych funkcji do listy liczb za pomocą 'map'.
    # numbers_to_process = [1, 2, 3]
    # processed_numbers = list(map(..., numbers_to_process))
    # print(f"Przetworzona lista: {processed_numbers}")
```

### Kod Rozwiązania

```python
from typing import Callable, List, Any

def compose(*functions: Callable[[Any], Any]) -> Callable[[Any], Any]:
    """
    Tworzy złożoną funkcję, która wykonuje podane funkcje w kolejności
    od prawej do lewej (jak w matematyce: f(g(x))).
    :param functions: Funkcje do skomponowania.
    :return: Skomponowana funkcja.
    """
    def composed_function(arg: Any) -> Any:
        result = arg
        for func in reversed(functions): # Od prawej do lewej
            result = func(result)
        return result
    return composed_function

def pipeline(*functions: Callable[[Any], Any]) -> Callable[[Any], Any]:
    """
    Tworzy złożoną funkcję (pipeline), która wykonuje podane funkcje w kolejności
    od lewej do prawej.
    :param functions: Funkcje do skomponowania.
    :return: Skomponowana funkcja.
    """
    def pipeline_function(arg: Any) -> Any:
        result = arg
        for func in functions: # Od lewej do prawej
            result = func(result)
        return result
    return pipeline_function

if __name__ == "__main__":
    # Przykładowe funkcje do kompozycji
    def add_five(x: int) -> int: return x + 5
    def multiply_by_two(x: int) -> int: return x * 2
    def to_string(x: int) -> str: return str(x) + "!"
    def capitalize_string(s: str) -> str: return s.upper()

    print("--- Kompozycja funkcji (f(g(x))) ---")
    # Obliczenie dla compose(capitalize_string, to_string, multiply_by_two, add_five):
    # input (x) -> add_five(x) -> multiply_by_two(...) -> to_string(...) -> capitalize_string(...)
    transform_data_composed = compose(capitalize_string, to_string, multiply_by_two, add_five)
    print(f"Wynik compose dla 3: {transform_data_composed(3)}") # Oczekiwany: '16!'

    print("\n--- Pipeline funkcji (f | g | h) ---")
    # Obliczenie dla pipeline(add_five, multiply_by_two, to_string, capitalize_string):
    # input (x) -> add_five(x) -> multiply_by_two(...) -> to_string(...) -> capitalize_string(...)
    transform_data_pipeline = pipeline(add_five, multiply_by_two, to_string, capitalize_string)
    print(f"Wynik pipeline dla 3: {transform_data_pipeline(3)}") # Oczekiwany: '16!'

    numbers_to_process = [1, 2, 3]
    # Zastosowanie skomponowanej funkcji do listy za pomocą map
    processed_numbers_composed = list(map(transform_data_pipeline, numbers_to_process))
    print(f"Przetworzona lista (pipeline): {processed_numbers_composed}") # Oczekiwany: ['12!', '14!', '16!']
```

---

## Zadanie 5: Zaawansowane Przetwarzanie Kolekcji z `reduce` i Immutability

### Kod Zadania (do uzupełnienia)

```python
from functools import reduce
from typing import List, Dict, Any

# Zadanie 5: Zaawansowane Przetwarzanie Kolekcji z 'reduce' i Immutability
# Cel: Mając listę obiektów 'Transaction', użyj funkcji 'reduce' do zagregowania danych
# w bardziej złożony sposób, na przykład do obliczenia salda konta i kategoryzacji transakcji.
# Upewnij się, że proces jest niezmienny, tj. nie modyfikuje oryginalnych obiektów
# ani pośrednich struktur danych akumulatora.

class Transaction:
    def __init__(self, type: str, amount: float):
        self.type = type # "deposit" or "withdrawal"
        self.amount = amount

    def __repr__(self):
        return f"Transaction(type='{self.type}', amount={self.amount})"

def calculate_balance_immutable(transactions: List[Transaction]) -> float:
    """
    Oblicza końcowe saldo konta na podstawie listy transakcji,
    zachowując niezmienność.
    """
    # TODO 1: Zdefiniuj funkcję redukującą (accumulator), która będzie przyjmować
    # aktualne saldo (accumulator) i pojedynczą transakcję.
    # Funkcja powinna zwracać nowe saldo.
    def accumulator(current_balance: float, transaction: Transaction) -> float:
        pass

    # TODO 2: Użyj `reduce` do zastosowania funkcji `accumulator` do listy transakcji.
    # Pamiętaj o początkowym saldzie (initial_value).
    initial_balance = 100.0
    final_balance = None
    return final_balance

def categorize_transactions_immutable(transactions: List[Transaction]) -> Dict[str, List[Transaction]]:
    """
    Kategoryzuje transakcje na depozyty i wypłaty, zwracając nową,
    niezmienną strukturę danych.
    """
    # TODO 3: Zdefiniuj funkcję redukującą, która będzie tworzyć słownik
    # z kategoryzowanymi transakcjami.
    # Pamiętaj o niezmienności: zawsze zwracaj nowy słownik/listę.
    def category_reducer(acc: Dict[str, List[Transaction]], transaction: Transaction) -> Dict[str, List[Transaction]]:
        # TODO 4: Wyjaśnij, dlaczego tutaj konieczne jest tworzenie NOWYCH kopii słownika i list.
        # Odpowiedź 4:
        pass

    # TODO 5: Zdefiniuj początkową wartość akumulatora (initial_categories).
    initial_categories = None

    # TODO 6: Użyj `reduce` do kategoryzacji transakcji.
    categorized_data = None
    return categorized_data

if __name__ == "__main__":
    transaction_list = [
        Transaction("deposit", 50.0),
        Transaction("withdrawal", 20.0),
        Transaction("deposit", 100.0),
        Transaction("withdrawal", 30.0),
        Transaction("deposit", 10.0)
    ]

    # TODO 7: Wywołaj calculate_balance_immutable i wydrukuj wynik.
    # final_account_balance = calculate_balance_immutable(transaction_list)
    # print(f"Końcowe saldo konta: {final_account_balance:.2f} zł")

    # TODO 8: Wywołaj categorize_transactions_immutable i wydrukuj wynik.
    # categorized_transactions = categorize_transactions_immutable(transaction_list)
    # print("Kategoryzowane transakcje:")
```

### Kod Rozwiązania

```python
from functools import reduce
from typing import List, Dict, Any

class Transaction:
    def __init__(self, type: str, amount: float):
        self.type = type # "deposit" or "withdrawal"
        self.amount = amount

    def __repr__(self):
        return f"Transaction(type='{self.type}', amount={self.amount})"

def calculate_balance_immutable(transactions: List[Transaction]) -> float:
    """
    Oblicza końcowe saldo konta na podstawie listy transakcji,
    zachowując niezmienność.
    """
    def accumulator(current_balance: float, transaction: Transaction) -> float:
        if transaction.type == "deposit":
            return current_balance + transaction.amount
        elif transaction.type == "withdrawal":
            return current_balance - transaction.amount
        return current_balance # Ignoruj nieznane typy transakcji

    initial_balance = 100.0 # Startowe saldo konta
    final_balance = reduce(accumulator, transactions, initial_balance)
    return final_balance

def categorize_transactions_immutable(transactions: List[Transaction]) -> Dict[str, List[Transaction]]:
    """
    Kategoryzuje transakcje na depozyty i wypłaty, zwracając nową,
    niezmienną strukturę danych.
    """
    def category_reducer(acc: Dict[str, List[Transaction]], transaction: Transaction) -> Dict[str, List[Transaction]]:
        # Odpowiedź 4: W programowaniu funkcyjnym dążymy do **niezmienności** (immutability).
        # Modyfikowanie 'acc' (słownika) lub list w nim bezpośrednio ('acc[key].append()')
        # zmieniałoby stan oryginalnego akumulatora, co jest **efektem ubocznym**.
        # Tworząc nową kopię słownika ({**acc}) i nową listę (old_list + [new_item]),
        # gwarantujemy, że każda iteracja reduce zwraca nowy, niezmienny stan,
        # zamiast modyfikować poprzedni.

        new_acc = {**acc} # Tworzymy NOWĄ kopię słownika

        # Tworzymy NOWĄ listę dla danego typu transakcji, zamiast modyfikować istniejącą
        if transaction.type in new_acc:
            new_acc[transaction.type] = new_acc[transaction.type] + [transaction]
        else:
            new_acc[transaction.type] = [transaction] # Nowa lista z pojedynczym elementem
        return new_acc

    initial_categories = {"deposit": [], "withdrawal": []} # Inicjalizuj puste listy
    categorized_data = reduce(category_reducer, transactions, initial_categories)

    return categorized_data

if __name__ == "__main__":
    transaction_list = [
        Transaction("deposit", 50.0),
        Transaction("withdrawal", 20.0),
        Transaction("deposit", 100.0),
        Transaction("withdrawal", 30.0),
        Transaction("deposit", 10.0)
    ]

    print("--- Obliczanie Salda (Niezmienność) ---")
    final_account_balance = calculate_balance_immutable(transaction_list)
    print(f"Końcowe saldo konta: {final_account_balance:.2f} zł") # Oczekiwany: 100 + 50 - 20 + 100 - 30 + 10 = 210 zł

    print("\n--- Kategoryzacja Transakcji (Niezmienność) ---")
    categorized_transactions = categorize_transactions_immutable(transaction_list)
    print("Kategoryzowane transakcje:")
    for category, txns in categorized_transactions.items():
        print(f"  {category.capitalize()}: {txns}")

    print(f"\nOryginalna lista transakcji pozostała niezmieniona: {transaction_list}")
```