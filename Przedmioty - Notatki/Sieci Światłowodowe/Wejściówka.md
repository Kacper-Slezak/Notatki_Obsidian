# Dyspersja w światłowodach

## Co to jest dyspersja?

Dyspersja to zjawisko, w którym różne składowe sygnału optycznego (np. różne długości fal) rozchodzą się w światłowodzie z różnymi prędkościami. Powoduje to:

- poszerzenie impulsu,
    
- zniekształcenie sygnału.
    

Jest to efekt kumulacyjny, który pogarsza się wraz z długością łącza.

Źródło: _CD_PMD.pdf_, sekcja 5.7 (strony 1–2)

---

## Składowe sygnału (kolory)

- To różne długości fal (częstotliwości) światła.
    
- Każda składowa może poruszać się z inną prędkością.
    
- Prowadzi to do rozmycia impulsu w czasie.
    

Źródło: _CD_PMD.pdf_, strona 1

---

## Przyczyny dyspersji

- Zależność prędkości grupowej od długości fali.
    
- Powoduje różne opóźnienia różnych składowych.
    

Źródło: _CD_PMD.pdf_, strona 1
 
---

## Rodzaje dyspersji

### Dyspersja materiałowa

- Zależność współczynnika załamania od długości fali.
    
- Różne fale → różne prędkości.
    

Źródło: _CD_measurement.pdf_, strona 1

### Dyspersja falowodowa

- Wynika ze struktury światłowodu.
    
- Różne mody światła mają różne prędkości grupowe.
    

W światłowodzie jednomodowym dominuje dyspersja chromatyczna.

Źródło: _CD_measurement.pdf_, strona 1

---

## Długość fali odcięcia

- Minimalna długość fali, przy której światłowód działa jako jednomodowy.
    
- Zależy od:
    
    - średnicy rdzenia,
        
    - różnicy współczynników załamania rdzenia i płaszcza.
        

Wzmianka: _CD_PMD.pdf_, strona 7

---

## Zero dyspersji chromatycznej

- Punkt, w którym dyspersja materiałowa i falowodowa się znoszą.
    
- Dyspersja chromatyczna = 0.
    

Dla standardowego SMF: około 1310 nm.

Źródła: _CD_PMD.pdf_ (strona 7), _CD_measurement.pdf_ (strona 3)

---

## Dyspersja polaryzacyjna (PMD)

- Różne prędkości grupowe dwóch ortogonalnych polaryzacji.
    
- Powodowana przez:
    
    - niedoskonałości geometryczne rdzenia (np. eliptyczność),
        
    - zmiany warunków zewnętrznych (losowa i zmienna w czasie).
        

Źródła: _CD_PMD.pdf_ (strony 5, 13–14), _PMD_measurement.pdf_ (strona 1)

---

## Porównanie dyspersji

|Rodzaj dyspersji|Wartość typowa|
|---|---|
|Chromatyczna|~17 ps/nm/km|
|Polaryzacyjna (PMD)|0,1–2 ps/√km|

Dyspersja chromatyczna ma znacznie większy wpływ niż PMD.

Źródło: _CD_PMD.pdf_, strona 14 (rys. 5.24)

---

## Pomiar dyspersji chromatycznej

### Metoda przesunięcia fazowego (Phase Shift Method)

- Mierzy się opóźnienie grupowe dla różnych długości fal.
    
- Oblicza się dyspersję jako pochodną opóźnienia względem długości fali.
    

Źródło: _CD_measurement.pdf_, strony 1–3

### Porównanie fazy

- Porównujemy fazę sygnału przed i po transmisji.
    
- Różnica fazy jest proporcjonalna do opóźnienia czasowego.
    

Źródło: _CD_measurement.pdf_, strona 2

### Śledzenie zmian fazy o 2π

- Trzeba unikać niejednoznaczności przy dużych zmianach fazy.
    
- Stopniowe dostrajanie długości fali pozwala śledzić zmiany.
    

Źródło: _CD_measurement.pdf_, strona 2

---

## Dobór częstotliwości modulacji

- Powinna być:
    
    - wystarczająco wysoka – dla czułości,
        
    - nie za wysoka – aby uniknąć wielokrotności 2π.
        

Przykład:  
Dla 40 km światłowodu i dyspersji 17 ps/nm/km odpowiednia częstotliwość to 1–10 GHz.

---
