
---

## 1. **Podstawowe Koncepcje**
### 1.1 Definicja Szyfrów Symetrycznych
- **Klucz**: Jeden tajny klucz używany do **szyfrowania i deszyfrowania**.
- **Zastosowania**: Szyfrowanie danych w spoczynku (np. dyski), komunikacja w czasie rzeczywistym (TLS).
- **Problemy**:
  - Bezpieczna dystrybucja klucza (wymaga protokołów asymetrycznych np. Diffie-Hellman).
  - Ryzyko ataków brute-force przy krótkich kluczach.

---

## 2. **Podział Szyfrów Symetrycznych**
### 2.1 Szyfry Strumieniowe
- **Działanie**: Generują **strumień klucza** (np. za pomocą LFSR), który jest XOR-owany z tekstem jawnym.
- **Przykłady**:
  - **RC4**: Używany w WEP (dziś niebezpieczny).
  - **ChaCha20**: Nowoczesny, stosowany w TLS 1.3.
- **LFSR (Linear Feedback Shift Register)**:
  - **Matematycznie**: Wielomian \( P(x) = x^4 + x + 1 \) definiuje sprzężenie zwrotne.
  - **Słabość**: Liniowość → podatność na ataki korelacyjne.

### 2.2 Szyfry Blokowe
- **Działanie**: Przetwarzają dane w **blokach** (np. 64/128 bitów).
- **Tryby Pracy**: ECB, CBC, CTR (omówione w sekcji 5).
- **Przykłady**:
  - **DES** (64-bitowy blok, 56-bitowy klucz).
  - **AES** (128-bitowy blok, klucze 128/192/256-bitowe).

---

## 3. **Własności Bezpiecznych Szyfrów**
| Własność                      | Opis                                                            | Przykład Implementacji                  |
| ----------------------------- | --------------------------------------------------------------- | --------------------------------------- |
| **Lawinowość**                | Zmiana 1 bitu tekstu jawnego zmienia ~50% bitów szyfrogramu.    | AES (MixColumns)                        |
| **Nieliniowość**              | Brak liniowych zależności między tekstem jawnym a szyfrogramem. | S-bloki w DES (nieliniowe podstawienia) |
| **Zupełność**                 | Każdy bit wyjściowy zależy od wszystkich bitów wejściowych.     | Permutacje w sieci Feistela             |
| **Niezależność międzybitowa** | Zmiana jednego bitu wpływa na losowość innych bitów.            | AES ShiftRows                           |

---

## 4. **Algorytmy Kluczowe**
### 4.1 **DES (Data Encryption Standard)**
- **Struktura**: Sieć Feistela z 16 rundami.
- **Klucz**: 56-bitowy (8 bitów parzystości).
- **Proces**:
  1. **Permutacja Początkowa (IP)**.
  2. Podział na **Lewą (L)** i **Prawą (R)** połowę (32 bity).
  3. Funkcja \( F(R, K_i) \):
     - **Rozszerzenie** z 32 do 48 bitów (E-blok).
     - XOR z **podkluczem** \( K_i \).
     - **S-bloki** (6 → 4 bity, nieliniowe podstawienie).
     - Permutacja P-blok.
  4. **Permutacja Końcowa (IP⁻¹)**.
- **Słabości**:
  - Klucz 56-bitowy → złamany w 1998 (EFF Deep Crack).
  - S-bloki projektowane z udziałem NSA (kontrowersje).

### 4.2 **Triple DES (3DES)**
- **Warianty**:
  - **3TDEA**: 3 klucze (168 bitów), szyfrowanie: \( E(K_1) → D(K_2) → E(K_1) \).
  - **2TDEA**: 2 klucze (112 bitów), mniej bezpieczny.
- **Zastosowania**: Systemy bankowe (np. EMV), zastąpiony przez AES.

### 4.3 **AES (Advanced Encryption Standard)**
- **Struktura**: **SPN (Substitution-Permutation Network)**.
- **Etapy w Rundzie**:
  1. **SubBytes**: Nieliniowe podstawienie za pomocą S-bloku (tabela 16x16).
  2. **ShiftRows**: Przesunięcie wierszy macierzy stanu.
  3. **MixColumns**: Mieszanie kolumn (mnożenie przez wielomian w \( GF(2^8) \)).
  4. **AddRoundKey**: XOR z podkluczem.
- **Liczba Rund**:
  - 10 (128-bitowy klucz), 12 (192-bitowy), 14 (256-bitowy).
- **Key Expansion**: Generowanie podkluczy z klucza głównego (algorytm Rijndael).

---

## 5. **Wyjaśnienie Trybów Szyfrów Blokowych**

---

## 1. **ECB (Electronic Codebook)**  
### **Schemat działania**  
- **Szyfrowanie**:  
  Każdy blok tekstu jawnego jest szyfrowany **niezależnie** za pomocą klucza.  
  [ECB](https://upload.wikimedia.org/wikipedia/commons/c/c4/ECB_encryption.svg)  
- **Deszyfrowanie**:  
  Każdy blok szyfrogramu jest deszyfrowany osobno.  

### **Cechy**  
- **Brak IV**: Nie używa wektora inicjalizacyjnego.  
- **Powtarzalność**: Te same bloki tekstu jawnego → te same bloki szyfrogramu (widoczne wzorce).  
- **Brak propagacji błędów**: Błąd w jednym bloku nie wpływa na inne.  
- **Zastosowania**: Tylko do krótkich danych (np. klucze sesyjne).  

---

## 2. **CBC (Cipher Block Chaining)**  
### **Schemat działania**  
- **Szyfrowanie**:  
  1. Pierwszy blok tekstu jawnego jest XOR-owany z **IV** (wektor inicjalizacyjny).  
  2. Wynik jest szyfrowany, tworząc pierwszy blok szyfrogramu.  
  3. Kolejne bloki są XOR-owane z poprzednim szyfrogramem przed szyfrowaniem.  
  ![CBC](https://upload.wikimedia.org/wikipedia/commons/8/80/CBC_encryption.svg)  
- **Deszyfrowanie**:  
  Każdy blok szyfrogramu jest deszyfrowany, a następnie XOR-owany z poprzednim szyfrogramem.  

### **Cechy**  
- **Wymaga IV**: Losowy wektor inicjalizacyjny (znany obu stronom).  
- **Propagacja błędów**: Błąd w bloku uszkadza **blok następny**.  
- **Ukrywa wzorce**: Tekst jawny jest "mieszany" z szyfrogramem.  
- **Zastosowania**: Szyfrowanie plików, TLS.  

---

## 3. **OFB (Output Feedback)**  
### **Schemat działania**  
- **Szyfrowanie**:  
  1. IV jest szyfrowany, tworząc **strumień klucza**.  
  2. Strumień klucza jest XOR-owany z tekstem jawnym.  
  3. Kolejne bloki strumienia generowane przez szyfrowanie poprzedniego strumienia.[OFB](https://upload.wikimedia.org/wikipedia/commons/f/f6/OFB_encryption.svg)  
- **Deszyfrowanie**:  
  Identyczne jak szyfrowanie (XOR strumienia klucza z szyfrogramem).  

### **Cechy**  
- **Brak propagacji błędów**: Błąd w szyfrogramie nie wpływa na inne bloki.  
- **Strumieniowy**: Konwersja szyfru blokowego na strumieniowy.  
- **Wymaga IV**: Ten sam IV i klucz → ten sam strumień klucza.  

---

## 4. **CFB (Cipher Feedback)**  
### **Schemat działania**  
- **Szyfrowanie**:  
  1. IV jest szyfrowany, tworząc strumień klucza.  
  2. Strumień klucza jest XOR-owany z tekstem jawnym, tworząc szyfrogram.  
  3. **Szyfrogram** staje się wejściem do kolejnej rundy (feedback).  
  ![CFB](https://upload.wikimedia.org/wikipedia/commons/9/9d/CFB_encryption.svg)  
- **Deszyfrowanie**:  
  Identyczne jak szyfrowanie (XOR strumienia klucza z szyfrogramem).  

### **Cechy**  
- **Propagacja błędów**: Błąd w bloku uszkadza **następny blok**.  
- **Strumieniowy**: Działa jak szyfr strumieniowy.  
- **Wymaga IV**: Losowy wektor inicjalizacyjny.  

---

## 5. **CTR (Counter)**  
### **Schemat działania**  
- **Szyfrowanie**:  
  1. Generowanie **licznika** (np. nonce + sekwencja numeryczna).  
  2. Licznik jest szyfrowany, tworząc strumień klucza.  
  3. Strumień klucza jest XOR-owany z tekstem jawnym.  
  [CTR](https://upload.wikimedia.org/wikipedia/commons/3/3d/CTR_encryption_2.svg)  
- **Deszyfrowanie**:  
  Identyczne jak szyfrowanie (XOR strumienia klucza z szyfrogramem).  

### **Cechy**  
- **Brak propagacji błędów**: Uszkodzony blok nie wpływa na inne.  
- **Równoległość**: Możliwość równoległego generowania strumienia klucza.  
- **Wymaga nonce**: Unikalna wartość dla każdego szyfrowania.  

---

## Podsumowanie: Porównanie Trybów  
| **Tryb** | **IV/nonce** | **Propagacja błędów** | **Strumieniowy** | **Bezpieczeństwo** |  
|----------|--------------|-----------------------|-------------------|---------------------|  
| **ECB**  | Nie          | Nie                   | Nie               | Niskie              |  
| **CBC**  | Tak          | Tak                   | Nie               | Średnie/Wysokie     |  
| **OFB**  | Tak          | Nie                   | Tak               | Wysokie             |  
| **CFB**  | Tak          | Tak                   | Tak               | Wysokie             |  
| **CTR**  | Tak (nonce)  | Nie                   | Tak               | Wysokie             |  

---

### **Kluczowe wnioski**  
- **ECB** jest **niezalecany** do długich danych ze względu na powtarzalność wzorców.  
- **CBC** i **CFB** są wrażliwe na propagację błędów, ale skutecznie ukrywają struktury danych.  
- **OFB** i **CTR** nadają się do transmisji strumieniowych (np. wideo), gdzie błędy są krytyczne.  
- **CTR** jest optymalny dla systemów wielowątkowych (równoległe przetwarzanie).  

___
### **Inne**

| Tryb    | Bezpieczeństwo                    | Wydajność | Uwagi                                                  |
| ------- | --------------------------------- | --------- | ------------------------------------------------------ |
| **ECB** | Niskie (powtarzalność wzorców)    | Wysoka    | Nieużywany do szyfrowania dużych danych (np. obrazów). |
| **CBC** | Wysokie (IV losowy)               | Średnia   | Wymaga wektora IV. Błąd w bloku wpływa na następne.    |
| **CTR** | Wysokie                           | Wysoka    | Brak propagacji błędów. Możliwość równoległości.       |
| **GCM** | Bardzo wysokie (uwierzytelnianie) | Średnia   | Używany w TLS 1.3 (np. AES-GCM).                       |

---

## 6. **Inne Algorytmy**
- **Blowfish**: 64-bitowe bloki, klucz do 448 bitów. Używany w OpenVPN.
- **Twofish**: Finalista konkursu AES, 128-bitowe bloki, klucz do 256 bitów.
- **ChaCha20**: Szyfr strumieniowy, alternatywa dla AES w urządzeniach IoT.

---

## 7. **Ataki i Bezpieczeństwo**
- **Atak Brute-Force**: DES (56 bitów) → \( 2^{56} \) kombinacji. AES-128 → \( 2^{128} \) (bezpieczny).
- **Atak Różnicowy**: DES podatny, AES odporny dzięki MixColumns i SubBytes.
- **Atak na Implementację**: Side-channel (np. pomiar czasu/poboru mocy). Rozwiązanie: Maskowanie.

---

## 8. **Podsumowanie: DES vs. AES**
| Parametr         | DES (1977)                     | AES (2001)                     |
|------------------|--------------------------------|--------------------------------|
| **Długość Klucza** | 56 bitów (niebezpieczny)       | 128/192/256 bitów             |
| **Blok**         | 64 bity                        | 128 bitów                     |
| **Bezpieczeństwo**| Złamany (1998)                 | Bezpieczny (FIPS 197)         |
| **Wydajność**    | 16 rund (wolniejszy)           | 10-14 rund (szybszy w hardware) |

---

## 9. **Przyszłość Szyfrów Symetrycznych**
- **Post-Kwantowe Standardy**: Algorytmy odporne na komputery kwantowe (np. AES-256 uważany za bezpieczny).
- **Lightweight Cryptography**: Optymalizacja dla IoT (np. SPECK, SIMON).