Jasne, Martyna! Uporządkujmy tę wiedzę, aby była maksymalnie przejrzysta i łatwa do przyswojenia.

Pojęcie **Batcha** (często tłumaczone jako "wsad" lub "partia") jest fundamentalne dla treningu sieci neuronowych. Poniżej znajdziesz sformatowane i czytelne wyjaśnienie tego mechanizmu.

---

# Czym jest Batch? (Wsad danych)

W uczeniu maszynowym **Batch** to po prostu **paczka danych**, którą sieć przetwarza jednocześnie w jednym kroku obliczeniowym.

Aby to zrozumieć, posłużmy się analogią budowlaną:

> **🧱 Analogia: Przenoszenie 1000 cegieł z punktu A do B**
> 
> 1. **Podejście pojedyncze (Stochastic):** Nosisz po **jednej** cegle w rękach.
>     
>     - _Efekt:_ Bardzo wolne, ciągłe kursowanie tam i z powrotem.
>         
> 2. **Podejście całościowe (Full Batch):** Próbujesz wziąć **wszystkie 1000** cegieł naraz.
>     
>     - _Efekt:_ Niemożliwe – nie masz tyle siły (pamięci RAM), cegły się rozsypią.
>         
> 3. **Podejście "Batch" (Mini-batch):** Bierzesz taczkę i wozisz po **32 cegły** na raz.
>     
>     - _Efekt:_ **Idealny kompromis**. Wykorzystujesz w pełni swoje narzędzie (taczkę), praca idzie szybko, a Ty się nie przeciążasz.
>         

W tej analogii **taczka to Twoja karta graficzna (GPU)**, a **liczba cegieł (32) to `batch_size`**.

---

## 1. Dlaczego nie uczymy na wszystkim naraz?

Podczas treningu sieć nie widzi całego zbioru danych (np. 100 000 zdjęć) w jednej chwili z dwóch powodów:

1. **💾 Pamięć (RAM/VRAM):** Karta graficzna ma ograniczoną pamięć. Nie zmieściłaby milionów parametrów sieci ORAZ wszystkich zdjęć jednocześnie.
    
2. **🚀 Szybkość (Równoległość):** GPU to bestie obliczeniowe stworzone do pracy równoległej. Przetworzenie 1 zdjęcia trwa prawie tyle samo, co 32 zdjęć naraz. Używanie batchy drastycznie przyspiesza proces.
    

### Słowniczek pojęć

- **Batch Size (Rozmiar partii):** Liczba przykładów w jednej paczce (np. 32, 64, 128).
    
- **Iteracja (Krok):** Przetworzenie jednego batcha (Obliczenie błędu $\rightarrow$ Aktualizacja wag).
    
- **Epoka:** Moment, w którym sieć zobaczyła (w kawałkach) już **wszystkie** przykłady ze zbioru dokładnie raz.
    

---

## 2. Operacje na Danych (Pipeline w TensorFlow)

W notatniku `tf.data.Dataset` działa jak taśma produkcyjna przygotowująca te paczki. Oto co robią poszczególne funkcje:

### A. `batch(size)` – Tworzenie paczek

To najważniejsza operacja techniczna. Zmienia ona wymiary danych (tensora).

- **Co robi:** Skleja pojedyncze przykłady w grupy.
    
- **Zmiana kształtu:**
    
    - Pojedyncze zdjęcie: `(28, 28, 3)` $\rightarrow$ (Wysokość, Szerokość, Kolor)
        
    - Po zbatchowaniu: `(32, 28, 28, 3)` $\rightarrow$ (**Indeks w paczce**, Wysokość, Szerokość, Kolor)
        
- **Cel:** Dzięki temu GPU może "połknąć" 32 zdjęcia na raz.
    

### B. `shuffle(buffer_size)` – Tasowanie

Krytyczne dla jakości nauki.

- **Problem:** Jeśli dane są posortowane (np. najpierw 1000 zdjęć kotów, potem 1000 psów), sieć w pierwszej fazie nauczy się, że "świat składa się tylko z kotów".
    
- **Rozwiązanie:** `shuffle` bierze grupę elementów do bufora i losuje z nich te, które trafią do batcha.
    
- **Efekt:** W jednym batchu masz wymieszane koty i psy. Uczenie jest **stabilne**, a gradient (kierunek nauki) bardziej wiarygodny.
    

### C. `prefetch(tf.data.AUTOTUNE)` – Przyspieszanie

Optymalizacja wydajności, działająca jak dobry kelner.

- **Problem:** GPU liczy szybciej niż CPU wczytuje dane z dysku. Bez `prefetch` GPU musiałoby czekać na dane ("nuda").
    
- **Rozwiązanie:**
    
    - Gdy GPU "trawi" (trenuje) **Batch nr 1**...
        
    - ...CPU w tle już przygotowuje i ładuje do pamięci **Batch nr 2**.
        
- **Efekt:** Zero przestojów. Utylizacja sprzętu wynosi 100%.
    

### D. `map()` – Przetwarzanie "w locie"

Używane do augmentacji (obracanie, przycinanie) lub normalizacji.

- **Działanie:** Aplikuje funkcję do każdego elementu. Dzięki batchowaniu operacja ta wykonywana jest na wielu elementach równolegle (wektoryzacja), co jest znacznie szybsze niż pętla `for`.
    

---

## 3. Podsumowanie w kodzie

Gdy w kodzie widzisz taką linijkę:

Python

```
dataset = dataset.shuffle(1000).batch(32).prefetch(tf.data.AUTOTUNE)
```

Oznacza to następujący proces:

1. 🔀 **Shuffle:** Weź 1000 przykładów do worka i wylosuj.
    
2. 📦 **Batch:** Sklej wylosowane przykłady w paczkę po 32 sztuki.
    
3. ⏩ **Prefetch:** Gdy model uczy się na bieżącej paczce, przygotuj już następną w tle.
    

**Czy ta forma notatki jest dla Ciebie czytelniejsza?**