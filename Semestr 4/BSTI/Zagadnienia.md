
---

### **Podstawy Bezpieczeństwa Systemów Teleinformatycznych**

- **Informacja:** Właściwość obiektów (fizyczna, strukturalna) lub ich wzajemna relacja, zinterpretowana przez odbiorcę i mająca dla niego znaczenie, dzięki czemu zmniejsza niewiedzę.
- **Dane:** Formalny opis informacji za pomocą odpowiednich symboli, dzięki czemu może być rejestrowana, przetwarzana i przesyłana.
- **Bezpieczeństwo:** Całokształt problemów związanych z ochroną danych zgromadzonych i przesyłanych między systemami informatycznymi. Poczucie braku zagrożenia.
- **Zakres Bezpieczeństwa (obejmuje kwestie):** zachowania poufności danych, weryfikacji tożsamości, protokołów komunikacyjnych, błędów w oprogramowaniu, nieprawidłowości w pracy administratorów i użytkowników sieci, problematyki nadużyć i ataków, nietechnicznych środków ochrony.

### **Wyzwania i Współzależności Bezpieczeństwa**

- **Wyzwania:**
    - **Złożoność:** Dotyczy software (np. jądro Linuxa), hardware (np. procesory AMD/Intel), oraz Internetu (np. liczba stron, wysyłanych maili).
    - **Wzajemne połączenia:** Wynikają z architektury rozproszonej, zdalnej pracy i Internetu.
    - **Dynamiczne zmiany:** Wymagają ciągłego łatania aplikacji i systemów, oraz aktualizacji programów antywirusowych.
    - **Wielowymiarowość:** Bezpieczeństwo może być postrzegane różnie w zależności od specjalizacji (np. kryptografia to szyfry, bezpieczeństwo informacji to znaki wodne/podpis cyfrowy).
    - **Różne typy sieci i systemów:** Różnią się wielkością (PAN, LAN, WAN, Internet), typem połączeń (przewodowe, bezprzewodowe), architekturą (klient-serwer, peer-to-peer), sposobem dostępu (intranet, połączenia wirtualne).
- **Współzależności:**
    - **Wydajność systemu spada** wraz ze wzrostem jego bezpieczeństwa.
    - **Koszt systemu rośnie** wraz ze wzrostem bezpieczeństwa.
    - **Problemy z administrowaniem i użytkowaniem** systemów ze zbyt wieloma usługami bezpieczeństwa.

### **Metodyczne i Całościowe Podejście do Ochrony**

- **Całościowe (holistyczne) podejście** do problematyki bezpieczeństwa jest właściwe.
- **Nieuinformatyczne sposoby ochrony:** alarmy, ochrona budynku, identyfikacja osób wchodzących.
- **Zabezpieczenia informatyczne:** uwierzytelnianie, szyfrowanie, wymiana kluczy, kontrola integralności, znakowanie czasem, autoryzacja.
- **Zabezpieczenia fizyczne:** architektura/konstrukcja obiektu, kontrola dostępu, ochrona przed włamaniami, ochrona PPOŻ, sąsiedztwo (np. pola magnetyczne).
- **Zabezpieczenia techniczne:** wybór sprzętu, redundancja, podtrzymanie zasilania (UPS), klimatyzacja, konserwacja/utrzymanie systemu.
- **Zabezpieczenia organizacyjno-administracyjne:** tryb postępowania (praca normalna/wyjątkowa), zakres obowiązków, uprawnienia dostępu, polityka kadrowa, podnoszenie kwalifikacji/szkolenia, dokumentacja/ewidencja, polityka bezpieczeństwa.

### **Architektura Bezpieczeństwa**

- **Wrażliwość na zagrożenia (vulnerability):** Wady lub słabości systemu, które mogą być wykorzystane do naruszenia jego bezpieczeństwa. Może być efektem złego zaprojektowania, implementacji, obsługi, konfiguracji lub innych wad.
- **Zagrożenia (threats):** Mają miejsce we wrażliwych systemach i mogą prowadzić do naruszenia ich bezpieczeństwa, np. zniszczenie, uszkodzenie, usunięcie danych, ujawnienie informacji, przerwanie komunikacji.
- **Atak:** Ma miejsce, kiedy konkretne zagrożenie występuje we wrażliwym systemie. Jest próbą naruszenia bezpieczeństwa przez osobę niepowołaną.
- **Metody ochrony danych:**
    - **Prywatność (privacy):** Prawo nadzorowania i dysponowania informacją o sobie, zachowania jej dla siebie lub udostępnienia określonym osobom.
    - **Poufność danych (data confidentiality):** Ograniczenie dostępu do danych, znane tylko pewnej grupie osób.
    - **Integralność danych (data integrity):** Właściwość danych gwarantująca wykrycie modyfikacji lub utraty części danych podczas transmisji.
    - **Uwierzytelnianie (authentication):** Potwierdzenie czyjejś tożsamości wobec innej jednostki.
    - **Kontrola dostępu (access control):** Ochrona przed nieuprawnionym dostępem do zasobów.
    - **Niezaprzeczalność (non-repudiation):** Zdolność udowodnienia, że dany podmiot wykonał określoną czynność.
    - **Dostępność/dyspozycyjność (availability):** Zapewnienie braku ograniczeń w dostępie do informacji, zasobów, usług czy działania aplikacji.
    - **Bezpieczny przepływ informacji (communication security):** Zapewnia wymianę danych między uprawnionymi jednostkami.
- **Warstwy bezpieczeństwa:** aplikacji, usług sieciowych, infrastruktury.
- **Płaszczyzny bezpieczeństwa:** zarządzania, sterowania, użytkownika.

### **Kryptografia Klasyczna**

- **Poufność:** Zapewniana przez ukrywanie (steganografia) lub szyfrowanie (kryptografia).
- **Steganografia:** Ukrywanie przesyłanych informacji, aby osoba postronna nie była świadoma ich istnienia. Przykłady: histiajos, atrament sympatyczny, mikrokropki. Współcześnie: ukrywanie w tekście (dodatkowe spacje, pierwsze litery), plikach multimedialnych (LSB), protokołach komunikacyjnych (nieużywane pola, czasy).
- **Szyfrowanie:** Przekształcenie poufnych danych do postaci nieczytelnej dla obcych osób bez odpowiedniego klucza.
- **Podstawowe pojęcia (kryptografia):** alfabet, tekst jawny, szyfrogram, szyfr, klucz, szyfrowanie, deszyfrowanie, kryptoanaliza, atak siłowy (brute-force).
- **Szyfry klasyczne:**
    - **Podstawieniowe:** Pojedynczy znak zastępowany innym. Mogą być proste (monoalfabetyczne, np. Szyfr Cezara, podatny na atak alfabetyczny/częstotliwość liter), homofoniczne (znak zastępowany z grupy homofonów), poligramowe (szyfrują grupy znaków, np. Szyfr Playfair), wieloalfabetowe (złożenie prostych szyfrów, np. Szyfr Vigenère’a, Szyfr Vernama, One-time pad).
    - **Przestawieniowe:** Kolejność znaków jest zmieniana, np. Szyfr zygzakowaty, transpozycje macierzy.
    - **Podstawieniowo-przestawieniowe:** Łączą podstawienie i przestawienie, np. Enigma.
- **Własności bezpiecznych szyfrów (wg Shanonna):**
    - **"Rozpraszanie" (diffusion):** Pojedynczy znak tekstu jawnego wpływa na wiele znaków szyfrogramu.
    - **"Zamieszanie" (confusion):** Ukrywanie związku między statystyką szyfrogramu a tekstem jawnym i kluczem.
- **Myśl przewodnia:** Kryptografia i steganografia mogą zapewnić poufność danych, ale poziom bezpieczeństwa zależy od użytego algorytmu.

### **Współczesne Szyfry Symetryczne**

- **Szyfry symetryczne:** Używają jednego tajnego klucza do szyfrowania i deszyfrowania. Są szybkie, ale problemem jest bezpieczna dystrybucja klucza.
- **Rodzaje szyfrów symetrycznych:**
    - **Strumieniowe:** Szyfrują po jednym bicie lub bajcie na raz.
    - **Blokowe:** Szyfrują jednocześnie cały blok bitów. Wymagają odpowiedniej długości bloku – zbyt mały blok jest niebezpieczny (zachowuje strukturę tekstu jawnego), zbyt duży wpływa na wydajność.
- **Wybrane własności bezpiecznych szyfrów (blokowych):**
    - **Zrównoważenie:** Szyfrogram powinien zawierać tyle samo zer co jedynek.
    - **Lawinowość:** Niewielkie zmiany na wejściu powodują duże zmiany na wyjściu (np. kryterium SAC - zmiana bitu wejściowego powoduje zmianę każdego bitu wyjściowego z prawdopodobieństwem ½).
    - **Nieliniowość:** Odporność na kryptoanalizę liniową.
    - **Zupełność:** Każdy bit wyjściowy zależy od każdego bitu wejściowego.
    - **Niezależność międzybitowa:** Zmiany bitów na wyjściu w wyniku zmiany pojedynczego bitu wejściowego są od siebie niezależne.
    - Odpowiedni rozkład wartości profilu XOR w S-bloku (ochrona przed kryptoanalizą różnicową).
    - Brak korelacji, pseudolosowy ciąg bitów.
- **Algorytm DES (Data Encryption Standard):** Opracowany w 1977 r.. Szyfruje bloki 64-bitowe kluczem 56-bitowym. Składa się z permutacji początkowej, 16 cykli (rund) wykorzystujących funkcję f (permutacja z rozszerzeniem, XOR z kluczem, podstawienie w S-blokach, permutacja w P-blokach), i permutacji końcowej. Problem: klucz 56-bitowy jest za krótki.
- **TripleDES (3DES):** Modyfikacja DES używająca dwóch kluczy (k1, k2). Szyfrowanie polega na: szyfrowanie kluczem k1, odszyfrowanie kluczem k2, szyfrowanie kluczem k1. C = EK1 [ DK2[ EK1(P) ] ].
- **Algorytm AES (Advanced Encryption Standard):** Standard FIPS-197. Wejście/wyjście: 128 bitów. Możliwe długości klucza: 128, 192 lub 256 bitów. Składa się z wielokrotnie powtarzanych podstawień i permutacji (10, 12 lub 14 rund), oraz dodawania klucza. Podstawowe funkcje: SubBytes(), ShiftRows(), MixColumns(), AddRoundKey().
- **Inne algorytmy symetryczne:** IDEA, SAFER, RC4, RC5, RC6, Blowfish, Twofish, Threefish, KASUMI, MILENAGE.
- **Tryby szyfrowania:** Określają, jak szyfrować duże ilości danych. Różnią się poziomem bezpieczeństwa, propagacją błędów i wydajnością. Przykłady: ECB (Electronic Codebook), CBC (Cipher Block Chaining), CFB (Cipher Feedback), OFB (Output Feedback), CTR (Counter).
- **Myśl przewodnia:** Szyfry symetryczne (np. AES) są wydajne, ale problem dystrybucji klucza generuje problem.

### **Szyfry Asymetryczne**

- **Kryptografia asymetryczna:** Używa pary kluczy: jawnego (publicznego) i tajnego (prywatnego). Klucz prywatny zna tylko właściciel, publiczny jest znany wszystkim. Dane zaszyfrowane jednym kluczem można odszyfrować tylko drugim. Główna zaleta: rozwiązuje problem dystrybucji klucza.
- **Schemat szyfrowania/podpisu cyfrowego:** Klucz publiczny służy do szyfrowania danych, klucz prywatny do ich deszyfrowania. Klucz prywatny służy do tworzenia podpisu cyfrowego, klucz publiczny do jego weryfikacji.
- **Szyfrowanie danych (np. w PGP):** Często łączy kryptografię symetryczną i asymetryczną, wykorzystując zalety obu.
- **Podstawy teorii liczb w kryptografii asymetrycznej:** Liczby pierwsze, arytmetyka modularna (a mod n = reszta), logarytm dyskretny (bx mod n = c), pierwiastek pierwotny modulo n.
- **Przykładowe algorytmy asymetryczne:** RSA (bazuje na potęgowaniu i operacji modulo), ElGamal (bazuje na logarytmach dyskretnych i operacji modulo).
- **Algorytm RSA:** Opracowany w 1978 r. przez Rivesta, Shamira, Adlemana. Bazuje na arytmetyce modulo n i liczbach pierwszych. Klucz publiczny to para liczb (e, n), klucz prywatny to liczba (d). Bezpieczeństwo RSA opiera się na trudności faktoryzacji dużych liczb (n=pq). Szyfrowanie: C = M^e mod n. Deszyfrowanie: M = C^d mod n.
- **Algorytm ElGamal:** Klucz publiczny to (q, a, y), klucz prywatny to x. y = a^x mod q. Bezpieczeństwo ElGamal opiera się na trudności obliczenia logarytmu dyskretnego. Szyfrowanie wiadomości M polega na obliczeniu C1 = a^k mod q i C2 = y^k * M mod q. Deszyfrowanie: M = C2 / (C1)^x mod q.
- **Inne algorytmy asymetryczne:** Krzywe eliptyczne, Rabin, McEliece, Chor-Rivest, Goldwaser-Micali.
- **Informowanie o kluczu publicznym:** Samodzielna dystrybucja i potwierdzanie wiarygodności lub za pomocą certyfikatu.
- **Certyfikat:** Plik podpisany cyfrowo przez zaufany podmiot (Urząd Certyfikacji), zawierający dane właściciela, jego klucz publiczny i informacje o wystawcy.
- **Współdzielony sekret (secret sharing):** Do ujawnienia sekretu (np. deszyfrowania) wystarczy zgoda części osób dzielących sekret. Przykładem są wielomiany interpolacyjne Lagrange’a.
- **Myśl przewodnia:** Szyfry asymetryczne (np. RSA) są mniej wydajne i zapewniają warunkowe bezpieczeństwo, ale rozwiązują problem dystrybucji klucza.

### **Integralność Danych i Generatory Liczb Losowych**

- **Integralność danych:** Zabezpiecza przed bezprawną modyfikacją danych.
- **Skrót wiadomości (hash):** Realizowany przez funkcję skrótu (haszującą), która przekształca dowolnie długi ciąg bitów na krótki ciąg binarny o ustalonej długości.
- **Własności funkcji skrótu:**
    - **Jednokierunkowość:** Łatwo obliczyć wartość skrótu, trudno obliczyć argument znając wartość.
    - **Odporność na kolizje:** Trudno znaleźć inny argument dający ten sam skrót (słaba odporność), trudno znaleźć dowolną parę wiadomości dających ten sam skrót (silna odporność).
    - Skrót zależy silnie od każdego bitu argumentu.
    - Wysoka wydajność.
    - Długość skrótu jest stała, niezależnie od długości wiadomości.
- **Kolizja:** Sytuacja, gdy dwie różne wiadomości (M1 ≠ M2) dają ten sam skrót (H(M1) = H(M2)).
- **Paradoks dnia urodzin:** W grupie 23 osób prawdopodobieństwo, że co najmniej dwie mają urodziny tego samego dnia, jest większe niż ½.
- **Atak metodą dnia urodzin:** Jeśli obliczymy nieco więcej niż 2^(n/2) skrótów (gdzie n to długość skrótu w bitach), prawdopodobieństwo znalezienia kolizji jest większe niż ½. Aby zapobiec, n powinno być >= 224.
- **Proste (niebezpieczne) przykłady funkcji skrótu:** Bit parzystości, skracanie ciągu binarnego, funkcje nieliniowe.
- **Funkcje skrótu:** Mogą być bez klucza (np. MD5, SHA) używane do podpisów cyfrowych lub z kluczem (np. MAC) używane do uwierzytelniania wiadomości.
- **Przykładowe funkcje skrótu:** MD5, SHA-1, SHA-2, SHA-3 (Keccak), RIPEMD-160, WHIRLPOOL.
- **SHA-2:** Używa 80 rund.
- **SHA-3:** Wybrany w konkursie NIST.
- **Zastosowania funkcji skrótu:** Kontrola integralności danych, uwierzytelnianie komunikatów, podpisy cyfrowe, przechowywanie skrótów haseł, definiowanie sygnatur/detekcja ataków, generatory liczb pseudolosowych, blockchain/kryptowaluty.
- **Hasła w systemach operacyjnych:** Często przechowywane w postaci skrótu ("zasolonego"). Zaleta/problem: hasła dostępu nie można odzyskać. Sól (salt) to dodatkowa losowa wartość dodawana przed haszowaniem, aby utrudnić ataki tęczowymi tablicami.
- **Generatory liczb losowych:** Wykorzystywane w kryptografii, symulacjach, metodzie Monte Carlo, grach. Prawdziwe źródła losowości: rozpad atomu, szum, odczyt stanu kwantowego.
- **Liczby pseudolosowe:** Generowane algorytmicznie (np. Blum Blum Shub). Większość komputerów używa generatorów pseudolosowych. Ważny wybór funkcji i ziarna. Standardowe biblioteki (np. rand()) mogą być niewystarczające w cyberbezpieczeństwie. Można wzmocnić źródło losowości ruchem myszki, zdarzeniami klawiatury, dynamicznymi danymi systemowymi (ps -ef, zegar, statystyki sieciowe). Wyjście słabego źródła można przepuścić przez dobrą funkcję skrótu (np. SHA-2).
- **Kryteria oceny losowości:** Dokumenty takie jak NIST SP 800-22 definiują szereg testów losowości ciągów binarnych (Frequency, Runs, Longest Run, Matrix Rank, DFT, Template Matching, Universal Statistical, Linear Complexity, Serial, Approximate Entropy, Cusum, Random Excursions).
- **Myśl przewodnia:** Jednokierunkowe funkcje skrótu (np. SHA-2) pomagają weryfikować integralność danych.

### **Certyfikaty i Infrastruktura Klucza Publicznego (PKI)**

- **Podpis elektroniczny:** Ponieważ klucz prywatny należy do konkretnej osoby, zaszyfrowanie dokumentu (lub jego skrótu) tym kluczem jednoznacznie potwierdza tożsamość podpisującego.
- **Własności podpisu elektronicznego:**
    - **Unikalność:** Każdy dokument ma unikalny podpis.
    - **Integralność:** Zmiana dokumentu unieważnia podpis.
    - **Niezaprzeczalność:** Tylko właściciel klucza prywatnego może wygenerować podpis.
- **Rodzaje podpisów:** Grupowe, ślepe.
- **Klucze publiczne:** Informowanie o wiarygodności klucza publicznego odbywa się poprzez samodzielną dystrybucję lub certyfikaty.
- **Certyfikat:** Plik podpisany cyfrowo przez Urząd Certyfikacji (CA), zawierający dane właściciela, klucz publiczny i informacje o wystawcy. Przykłady: certyfikaty PGP i X.509.
- **Infrastruktura Klucza Publicznego (PKI):** Zespół elementów (urządzenia, oprogramowanie, procedury, polityki, osoby) umożliwiający bezpieczne używanie kluczy publicznych w formie certyfikatów cyfrowych. Umożliwia tworzenie, przechowywanie, zarządzanie i rozprowadzanie certyfikatów.
- **Struktura PKI:** Składa się z Urzędów Rejestracji (RA), Urzędów Certyfikacji (CA), Repozytoriów certyfikatów i list unieważnionych certyfikatów (CRLs).
- **Urząd Certyfikacji (CA):** Wydaje certyfikaty klucza publicznego, podpisując je swoim kluczem prywatnym. Certyfikaty automatycznie chronią integralność danych. Postać CA zależy od modelu zaufania.
- **Urząd Rejestracji (RA):** Weryfikuje dane użytkownika przed rejestracją. Może być zintegrowany z CA lub wyodrębniony przy dużej liczbie użytkowników.
- **Funkcje PKI:** Rejestracja, Certyfikacja, Generacja kluczy, Odnawianie kluczy (upłynięcie ważności, kompromitacja klucza), Certyfikacja wzajemna, Odwołanie certyfikatu, Odzyskiwanie klucza.
- **Cykl życia certyfikatu:** Rejestracja -> Generowanie kluczy -> Tworzenie/dystrybucja certyfikatu -> Rozpowszechnienie -> Kopia bezpieczeństwa (opcja) -> Odwołanie lub upływ terminu -> Odnowienie/aktualizacja -> Historia kluczy.
- **Unieważnienie certyfikatu:** PKI musi pozwalać na unieważnienie certyfikatu przed upływem ważności (np. ujawnienie klucza, zmiana danych, zwolnienie). Sposoby: okresowe publikowanie list unieważnionych certyfikatów (CRL) lub protokoły kontroli stanu (OCSP).
- **Lista unieważnionych certyfikatów (CRL):** Struktura danych z listą unieważnionych certyfikatów. Podpisana cyfrowo przez CA. Publikowana w ogólnodostępnym miejscu (LDAP, FTP, HTTP). Zawiera m.in. wersję, identyfikator algorytmu, wydawcę, daty wydania/kolejnej listy, listę unieważnionych certyfikatów, opcjonalne rozszerzenia. Certyfikaty często wskazują punkt dystrybucji CRL.
- **Protokół OCSP (Online Certificate Status Protocol):** Protokół żądanie-odpowiedź do sprawdzania ważności certyfikatu. Wymaga zaufanego respondenta OCSP, który odsyła cyfrowo podpisane odpowiedzi. Informuje tylko, czy certyfikat został unieważniony. Wymaga dostępu do sieci.
- **Wiele certyfikatów na jednostkę:** Możliwe dla zróżnicowania poziomów bezpieczeństwa (np. różne klucze do podpisu i szyfrowania). Każdy klucz wymaga osobnego certyfikatu. Ten sam klucz może być certyfikowany przez kilka CA.
- **Rozpowszechnianie certyfikatów:** Prywatne (użytkownicy przesyłają sobie wzajemnie, np. PGP) lub poprzez repozytoria (publiczne miejsca, np. serwer LDAP, FTP, HTTP; wymaga zadbania o dostępność - ochrona przed DoS).
- **PKI vs. prywatność:** Certyfikaty mogą zawierać dane osobowe, informacje o strukturze firmy, odwołania mogą zdradzać zmiany kadrowe. Rozwiązanie: anonimowe certyfikaty bez danych osobowych.
- **Znakowanie czasem (Time-Stamping):** Niezaprzeczalny dowód istnienia informacji w określonym czasie. Czas pobierany z wewnętrznego zegara lub zaufanego Serwera Czasu.
- **Modele zaufania w PKI:** Oparty na użytkowniku (np. PGP), ścisła hierarchia CA, luźna hierarchia CA, model sieci www, rozproszony model zaufania.
- **Certyfikacja wzajemna (cross-certification):** Pozwala użytkownikom z jednej struktury PKI ufać certyfikatom z innej struktury. Główne CA z dwóch struktur certyfikują się wzajemnie (jednokierunkowo lub dwukierunkowo).
- **Przetwarzanie ścieżki certyfikatu:** Budowa ścieżki (znalezienie łańcucha do zaufanego klucza) i zatwierdzenie ścieżki (sprawdzenie ważności każdego certyfikatu). Może być trudne przy wielu certyfikatach wzajemnych.
- **Kwalifikowany podpis elektroniczny w Polsce:** Ma skutki prawne równoważne podpisowi własnoręcznemu. Używanie danych do podpisu innej osoby jest karalne.
- **Podpis elektroniczny w Europie:** Regulowany dyrektywą 1999/93/WE i rozporządzeniem (UE) NR 910/2014. Polska ma Zaufaną Listę akredytowanych Podmiotów świadczących usługi certyfikacyjne (TSL). Komisja Europejska publikuje centralną "listę list".
- **Narodowe Centrum Certyfikacji:** System NBP realizujący zadania związane z usługami zaufania (wytwarzanie/wydawanie zaświadczeń certyfikacyjnych, publikacja list wydawanych/unieważnionych zaświadczeń).
- **Urządzenia do składania podpisu elektronicznego:** Karta kryptograficzna (nośnik certyfikatu), czytnik kart, komputer z oprogramowaniem.
- **Czego nie robi PKI:** Nie zapewnia zaufania do jednostki (tylko do klucza), nie nadaje nazw jednostkom (dane w certyfikacie zależą od wystawcy), nie koryguje błędnych zachowań użytkowników, jest tylko częścią zabezpieczeń.
- **Przyszłość PKI:** Potrzeba uproszczenia, budowania zaufania bez wysokich kosztów, problem nieświadomości/lenistwa użytkowników, kryzys zaufania do nadrzędnych jednostek.
- **Myśl przewodnia:** Certyfikat wiąże klucz publiczny i jego właściciela, co pozwala jednoznacznie określić autora podpisu cyfrowego i/lub odbiorcę poufnych danych.

### **Ustalanie Kluczy Kryptograficznych i VPN**

- **Bezpieczna wymiana kluczy:** Konieczna w przypadku szyfrów symetrycznych. Zbyt długie używanie tego samego klucza grozi rozszyfrowaniem wiadomości. Wymiana na nowe klucze poprawia bezpieczeństwo. Klucz sesji jest używany do szyfrowania danych, klucz nadrzędny do ochrony kluczy sesyjnych.
- **Wymiana typu punkt-punkt:** Jednoetapowa (np. szyfrowanie klucza sesji kluczem publicznym odbiorcy, jak w GPG) lub trójetapowa (Challenge-Response).
- **Centrum Dystrybucji Kluczy (KDC):** Wyspecjalizowana jednostka wybierająca i rozsyłająca klucze sesyjne. Zmniejsza liczbę kluczy do przechowywania (równa liczbie użytkowników). Przykład protokołu: Kerberos.
- **Algorytm Shamira (Shamir Three-pass Protocol, Shamir No-Key Protocol):** Przykład ustalania kluczy bez klucza nadrzędnego/KDC. Umożliwia ustalenie wspólnego klucza K między A i B poprzez wymianę trzech wiadomości, wykorzystując ich sekretne liczby a i b oraz jawną liczbę pierwszą p.
- **Algorytm Diffiego-Hellmana:** Umożliwia dwóm stronom (A i B) ustalenie wspólnego tajnego klucza poprzez wymianę informacji jawnych, bazując na ich prywatnych (tajnych) liczbach. Wymaga wspólnego wyboru dużej liczby pierwszej p i pierwiastka pierwotnego modulo p (g). Wada: podatny na atak "man in the middle". Modyfikacje: protokoły STS, MTI.
- **Uczenie maszynowe (neural cryptography):** Przy użyciu sieci neuronowych (TPM) i algorytmów uczenia maszynowego można projektować protokoły ustalania poufnych kluczy.
- **Problem protokołów ustalania/dystrybucji kluczy:** Narażone na ataki, szczególnie bierny podsłuch (użytkownicy często nie są świadomi). Rozwiązanie (potencjalne): Kryptografia kwantowa.
- **VPN (Virtual Private Network):** Pozwala bezpiecznie łączyć sieci i komputery poprzez niezaufane medium (Internet, linie dzierżawione). Komunikacja jest szyfrowana, tworzone są wirtualne tunele.
- **Rodzaje VPN:** Oparte na IPsec (site-to-site, remote-access/client-to-site), oparte na SSL, oparte na innych protokołach (PPTP, L2TP, Hamachi).
- **IPsec:** Protokół ochrony informacji w sieciach komputerowych, blisko związany z warstwą sieci (IP). Zapewnia poufność i integralność danych. Definiuje nagłówki: AH (Authentication Header) i ESP (Encapsulation Security Payload).
- **IPsec - AH (Authentication Header):** Zapewnia ochronę integralności danych i części nagłówka IP (pola, które nie zmieniają się w trasie). Wykorzystuje funkcje skrótu (np. SHA).
- **IPsec - ESP (Encapsulation Security Payload):** Zapewnia szyfrowanie danych ORAZ ochronę ich integralności (tylko dla danych użytecznych). Szyfrowanie np. algorytmem AES. Funkcje skrótu podobnie jak w AH.
- **Tryby pracy protokołu IPsec:** Transportowy, tunelowy.
- **Myśl przewodnia:** Sieć VPN buduje prywatne połączenia w publicznej infrastrukturze dzięki użytym algorytmom kryptograficznym.

### **Uwierzytelnianie i Autoryzacja**

- **Uwierzytelnianie (Authentication):** Zaświadczenie jednostki o swojej tożsamości. Etapy: identyfikacja (np. login) i weryfikacja (np. sprawdzenie hasła).
- **Środki uwierzytelniania ("trzy czynniki"):**
    - **Indywidualna wiedza ("to co wiem"):** Hasło, PIN.
    - **Unikalna rzecz ("to co posiadam"):** Karta, token, telefon (SMS).
    - **Cechy biometryczne ("to czym jestem" / "to jak się zachowuję"):** Statyczna (linie papilarne, tęczówka) lub dynamiczna (głos, chód).
- **Aspekty bezpieczeństwa uwierzytelniania:** Wzajemne vs. jednokierunkowe, wielopoziomowe/wieloskładnikowe (np. w bankowości, PSD2). Poufność procesu (szyfrowana komunikacja), aktualność użytych danych.
- **Ochrona przed atakami powtórzeniowymi:** Numery sekwencyjne, znaczniki czasowe, identyfikatory żądania.
- **Hasła:** Tanie, trudne do zgadnięcia (zwykle), łatwe do zapamiętania/zmiany/konfiguracji, przenośne. Typy: stałe, jednorazowe (SMS, listy, token), "mieszane" ('macierze', wybrane znaki hasła stałego). Problemy: przechowywanie (należy przechowywać skróty, nie hasła), co jeśli intruz uzyska dostęp do skrótów (solenie hasła utrudnia).
- **Sól (salt):** Losowa wartość dodawana do hasła przed haszowaniem. Skróty haseł są przechowywane wraz z solą (np. w `/etc/shadow` w Linuksie). Solenie utrudnia ataki słownikowe i tęczowymi tablicami.
- **Typ uwierzytelniania challenge-response:** Odpowiedź obliczana na podstawie żądania (challenge), adresu urządzenia i tajnego klucza. Przykład: uwierzytelnianie Bluetooth.
- **Karty inteligentne:** Przenośne, trudne do podrobienia. Zawierają mikroprocesor, pamięć RAM/ROM/FLASH.
- **RFID (Radio Frequency Identification):** Następca kodów kreskowych z zaletami: unikalna identyfikacja obiektu, automatyczna identyfikacja. Zastosowania: zarządzanie dokumentami, śledzenie zasobów, kontrola dostępu/parkingów, identyfikacja bagażu, systemy biletowe.
- **Uwierzytelnianie za pomocą kryptografii asymetrycznej:** Opiera się na parze kluczy (tajny i publiczny). Jeśli wiadomość została zaszyfrowana kluczem tajnym, oznacza to, że zrobił to jego właściciel.
- **Protokół Lamporta:** Protokół uwierzytelniania jednorazowym hasłem. Obie strony znają początkową tajną wartość x0 i stosują na niej wielokrotnie funkcję jednokierunkową, tworząc ciąg x0, x1, ..., xn. Użytkownik wysyła login (xi), system sprawdza na liście skrótów, prosi o xi-1, użytkownik wysyła xi-1, system sprawdza czy skrót z xi-1 (H(xi-1)) jest równy xi.
- **Biometria:** Używa cech biologicznych (linie papilarne, tęczówka, głos, kształt twarzy/dłoni/ucha, układ naczyń krwionośnych, chód, pisanie na klawiaturze, zapach, DNA, ruch gałki oka, fala P300). Technika bezpieczna, ale kosztowna.
- **Linie papilarne:** Nie ma dwóch osób z identycznymi liniami.
- **Tożsamość federacyjna:** Umożliwia logowanie do wielu usług (Service Providers) przy użyciu jednych danych uwierzytelniających z jednego dostawcy tożsamości (Id Provider), bazując na cyklu zaufania (Cycle of trust) i umożliwiając Single-Sign-On.
- **Autoryzacja (Authorization):** Proces przydzielania (lub odmowy) praw dostępu do poszczególnych zasobów. Następuje zwykle po uwierzytelnieniu.
- **Zróżnicowanie praw dostępu:** Indywidualne dla użytkowników lub poprzez grupy z typowymi prawami (np. Administrator, Użytkownik, Gość).
- **Autoryzacja w systemach Unix/Linux:** Bazuje na różnicowaniu praw dla 3 grup (właściciel, grupa, pozostali) i 3 typów działania (czytanie, zapisywanie, uruchamianie).
- **Myśl przewodnia:** Uwierzytelnianie potwierdza tożsamość, a autoryzacja przydziela lub odmawia praw dostępu do zasobów.

### **Systemy Wykrywania Zagrożeń**

- **Podstawowe narzędzia ochrony (chronologicznie):** Zapora sieciowa (Firewall), IDS/IPS/IDPS, NGFW (Next-Generation Firewall), SIEM (Security Information and Event Management), SOAR (Security Orchestration, Automation, and Response), AV (Antivirus), Honey pot.
- **Warstwy ochrony:** NIDS (skanowanie ruchu sieciowego), AV (analiza kodu), HIDS (analiza zachowania procesów), Sandbox (izolacja/wirtualizacja).
- **Zapora sieciowa / Firewall:** Filtrowanie pakietów na podstawie reguł. Generacje: bezstanowe (pakiety/warstwa 3 OSI), stanowe (połączenia/warstwa 4 OSI), monitorujące aplikacje (aplikacje/protokoły/wyższe warstwy OSI).
- **Reguły:** Pojedynczy wpis filtrujący. **Polityka bezpieczeństwa:** Spójny zestaw reguł. **ACL (Access Control List):** Pojęcie szersze niż firewalle/IDPS, ale często stosowane.
- **Sprawdzane elementy przez firewalle:** Źródłowy/docelowy adres IP, źródłowy/docelowy port, protokół warstwy wyższej, interfejs urządzenia. Akcja po dopasowaniu: alarm, usunięcie pakietu, rozłączenie.
- **Zapory otwarte i zamknięte (domyślna akcja):** Otwarte (wszystko, co nie zabronione, jest dozwolone). Zamknięte (wszystko, co nie dozwolone, jest zabronione).
- **Segmenty sieci:** Podział sieci na strefy (zewnętrzna, wewnętrzna, DMZ). **DMZ (strefa zdemilitaryzowana):** Wydzielona strefa o mniej restrykcyjnej polityce (serwery www, FTP, poczta, DNS).
- **Intrusion Detection/Prevention System (IDPS):** Monitorowanie zdarzeń w systemie/sieci w celu wykrycia intruzów/zapobiegania atakom.
- **Dwa główne podejścia do wykrywania zagrożeń/włamań:**
    - **Sygnatury ataków:** Porównanie do wzorca. Efektywne dla znanych ataków, pewne, szybkie, precyzyjne. Można tworzyć własne sygnatury. Brak skalowalności dla wirusów polimorficznych.
    - **Wykrywanie anomalii:** Porównanie do typowego ruchu. Wykrywa nawet nieznane ataki. Zwykle wymaga wzorca ruchu (trenowanie). Potencjalnie skalowalne. Generuje dużą ilość fałszywych alarmów (false positives).
- **False positives:** Normalne zachowanie systemu zakwalifikowane jako atak przez system IDS.
- **Przykładowe metryki do wykrywania anomalii:** Dla użytkowników (częstotliwość/czas logowania, IP źródłowe, czas sesji, rozmiar danych, zużycie zasobów, liczba niepoprawnych logowań). Dla programów/aplikacji (częstotliwość uruchamiania, zużycie zasobów, odczyt/zapis plików, liczba odrzucanych żądań dostępu).
- **Inne podejścia:** Heurystyka (zachowanie), Sztuczna inteligencja.
- **Aplikacje IDS (przykłady darmowych):** Snort (NIDS), OSSEC (HIDS).
- **Snort:** Popularny NIDS. Reguły składają się z nagłówka (akcja, protokół, adres/port źródłowy/docelowy, kierunek) i opcji (komunikat, flagi TCP, zawartość binarna/tekstowa, referencje, ID reguły, typ klasy, numer wersji).
- **Typowa architektura bezpieczeństwa:** Podział sieci na strefy, podział zasobów na grupy (np. serwery), podział zagrożeń na grupy.
- **Problemy otwarte (z firewalls/IDPS):** Brak ochrony przed zagrożeniami wewnętrznymi/innymi drogami komunikacji. Systemy mogą stać się celem ataków (blokowanie portów). Dostosowanie do konkretnej sieci. Utrzymanie systemu (wymaga rozsądnego administratora). Ogromna ilość logów.
- **Zapory/IDPS w chmurze:** Zalety: odporność na awarie, opłaty za zużycie, skalowalność. SECaaS (Security-as-a-Service). Wyzwania: wydajność vs. poufność. Problem poufności polityki bezpieczeństwa w chmurze publicznej. Anonimizacja polityki bezpieczeństwa (np. filtry Blooma).
- **Szyfrowanie homomorficzne:** Umożliwia wykonywanie operacji na szyfrogramach. Przykład w RSA: C1 * C2 = (M1 * M2)^e mod n.
- **SIEM (Security Information and Event Management):** Centralny system wykrywania zagrożeń zbierający informacje z wielu urządzeń/systemów. Umożliwia korelację zdarzeń w sieci. Przykłady: Splunk ES, IBM Qradar, OSSIM, ELK Stack.
- **Bezpieczeństwo systemu (elementy):** firewall, uwierzytelnianie, kontrola dostępu, antywirus, IDPS, wykrywanie anomalii, SIEM, honey pot. Kluczowy element: rozsądny administrator.
- **Myśl przewodnia:** Podstawowe sposoby wykrywania zagrożeń/ataków to porównanie do wzorca (sygnatury) i porównanie do typowego ruchu (anomalie).

---

