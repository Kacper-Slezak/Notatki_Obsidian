# Identyfikacja Ukrytych Trybów Szyfrowania w AESCipher

Aby zidentyfikować ukryte tryby szyfrowania w aplikacji **AESCipher**, możemy przeanalizować ich **charakterystyczne cechy** i porównać je z właściwościami znanych trybów szyfrowania (ECB, CBC, OFB, CFB, CTR). Poniżej znajduje się szczegółowa analiza, która pozwala na identyfikację każdego z trybów.

---

## 1. **Tryb 1: ECB (Electronic Codebook)**  
### **Charakterystyka**  
- **Brak IV**: Nie używa wektora inicjalizacyjnego.  
- **Powtarzalność**: Te same bloki tekstu jawnego dają **identyczne bloki szyfrogramu**.  
- **Brak propagacji błędów**: Błąd w jednym bloku nie wpływa na inne.  

### **Identyfikacja**  
- Jeśli w aplikacji widzisz, że **identyczne bloki danych** są szyfrowane do **identycznych bloków szyfrogramu**, to jest to **ECB**.  

---

## 2. **Tryb 2: CBC (Cipher Block Chaining)**  
### **Charakterystyka**  
- **Wymaga IV**: Używa wektora inicjalizacyjnego (IV).  
- **Propagacja błędów**: Błąd w jednym bloku wpływa na **następne bloki**.  
- **Zależność między blokami**: Każdy blok jest XOR-owany z poprzednim szyfrogramem przed szyfrowaniem.  

### **Identyfikacja**  
- Jeśli aplikacja wymaga podania **IV** i widzisz, że **błąd w jednym bloku** wpływa na kolejne, to jest to **CBC**.  

---

## 3. **Tryb 3: OFB (Output Feedback)**  
### **Charakterystyka**  
- **Wymaga IV**: Używa wektora inicjalizacyjnego.  
- **Brak propagacji błędów**: Błąd w jednym bloku nie wpływa na inne.  
- **Strumieniowy**: Generuje strumień klucza niezależnie od tekstu jawnego.  

### **Identyfikacja**  
- Jeśli aplikacja wymaga **IV**, a błędy w szyfrogramie **nie wpływają na inne bloki**, to jest to **OFB**.  

---

## 4. **Tryb 4: CFB (Cipher Feedback)**  
### **Charakterystyka**  
- **Wymaga IV**: Używa wektora inicjalizacyjnego.  
- **Propagacja błędów**: Błąd w jednym bloku wpływa na **następne bloki**.  
- **Strumieniowy**: Działa jak szyfr strumieniowy, ale zależny od poprzedniego szyfrogramu.  

### **Identyfikacja**  
- Jeśli aplikacja wymaga **IV**, a błędy w szyfrogramie **wpływają na kolejne bloki**, to jest to **CFB**.  

---

## 5. **Tryb 5: CTR (Counter)**  
### **Charakterystyka**  
- **Wymaga nonce**: Używa unikalnej wartości (nonce) zamiast IV.  
- **Brak propagacji błędów**: Błąd w jednym bloku nie wpływa na inne.  
- **Równoległość**: Możliwość równoległego przetwarzania.  

### **Identyfikacja**  
- Jeśli aplikacja wymaga **nonce** (np. licznika), a błędy w szyfrogramie **nie wpływają na inne bloki**, to jest to **CTR**.  

---

## 6. **Tryb 6: CBC-MAC (Cipher Block Chaining Message Authentication Code)**  
### **Charakterystyka**  
- **Wymaga IV**: Używa wektora inicjalizacyjnego (często zerowego).  
- **Skrót kryptograficzny**: Wynikiem jest **ostatni blok szyfrogramu**.  
- **Bezpieczeństwo**: Używany do uwierzytelniania wiadomości.  

### **Identyfikacja**  
- Jeśli aplikacja generuje **skrót kryptograficzny** (np. 128-bitowy) z danych wejściowych, to jest to **CBC-MAC**.  

---

## Podsumowanie: Identyfikacja Trybów w AESCipher  
| **Tryb**   | **Wymaga IV/nonce** | **Propagacja błędów** | **Strumieniowy** | **Skrót kryptograficzny** |  
|------------|---------------------|-----------------------|-------------------|---------------------------|  
| **ECB**    | Nie                 | Nie                   | Nie               | Nie                       |  
| **CBC**    | Tak (IV)            | Tak                   | Nie               | Nie                       |  
| **OFB**    | Tak (IV)            | Nie                   | Tak               | Nie                       |  
| **CFB**    | Tak (IV)            | Tak                   | Tak               | Nie                       |  
| **CTR**    | Tak (nonce)         | Nie                   | Tak               | Nie                       |  
| **CBC-MAC**| Tak (IV)            | Tak                   | Nie               | Tak                       |  

---

### **Jak to działa w praktyce?**  
1. **ECB**: Jeśli widzisz, że identyczne bloki danych dają identyczne szyfrogramy, to jest to **ECB**.  
2. **CBC**: Jeśli aplikacja wymaga IV, a błędy w jednym bloku wpływają na kolejne, to jest to **CBC**.  
3. **OFB**: Jeśli aplikacja wymaga IV, a błędy nie wpływają na inne bloki, to jest to **OFB**.  
4. **CFB**: Jeśli aplikacja wymaga IV, a błędy wpływają na kolejne bloki, to jest to **CFB**.  
5. **CTR**: Jeśli aplikacja wymaga nonce (licznika), a błędy nie wpływają na inne bloki, to jest to **CTR**.  
6. **CBC-MAC**: Jeśli aplikacja generuje skrót kryptograficzny, to jest to **CBC-MAC**.  

---

### **Wniosek**  
Poprzez analizę cech takich jak:  
- **Wymaganie IV/nonce**,  
- **Propagacja błędów**,  
- **Generowanie skrótu kryptograficznego**,  
można jednoznacznie zidentyfikować każdy z ukrytych trybów w aplikacji **AESCipher**.

___
# Pytanie 2: Czy ten sam algorytm i klucz dadzą identyczny szyfrogram w różnych trybach?

**Nie**, nawet przy użyciu tego samego algorytmu i klucza, różne tryby szyfrowania generują **inne szyfrogramy**.

**Dlaczego?**

1. **Różnice strukturalne między trybami**:
   - Tryby takie jak **ECB** szyfrują bloki niezależnie, podczas gdy **CBC** wprowadza zależność między blokami (XOR z poprzednim szyfrogramem).
   - Tryby strumieniowe (**OFB**, **CFB**, **CTR**) generują klucz dynamicznie, zależny od IV/nonce.

2. **Rola IV/nonce**:
   - Tryby z IV (np. CBC, CFB) wymagają losowego wektora inicjalizacyjnego, który jest częścią procesu szyfrowania. Nawet ten sam IV w różnych trybach da inne wyniki.

3. **Bezpieczeństwo determinizmu**:
   - Tylko **ECB** (bez IV) może teoretycznie dać ten sam szyfrogram dla tych samych danych, ale nawet wtedy inne tryby zmieniają logikę przetwarzania.

**Przykład**:
- Tekst jawny: `[Blok1, Blok2]`
- **ECB**: `Szyfr(Blok1), Szyfr(Blok2)` (brak zależności między blokami).
- **CBC**: `Szyfr(Blok1 ⊕ IV), Szyfr(Blok2 ⊕ Wynik_Blok1)` (IV i zależność między blokami).
- **CTR**: `Blok1 ⊕ Strumień_Klucza, Blok2 ⊕ Strumień_Klucza` (strumień generowany z licznika).

**Wniosek**: Tryb szyfrowania definiuje **logikę przetwarzania danych**, dlatego różne tryby nigdy nie dadzą identycznych szyfrogramów, nawet przy tych samym kluczu i algorytmie.