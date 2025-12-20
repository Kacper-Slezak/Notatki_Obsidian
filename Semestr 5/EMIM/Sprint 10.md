## **6. Plan na Kolejny Sprint**

W następnym sprincie planowane jest:

- Zdefiniowanie i spisanie zestawu nieoficjalnych modyfikacji zasad używanych w testach.
- Przystosowanie promptów / interfejsu tak, aby klarownie komunikowały nowe reguły Peterowi.
- Przeprowadzenie serii gier testowych z modyfikacjami i analiza, na ile model modyfikuje swoją strategię względem „standardowej” Diuny.


Test czy strategia jest ściągnięta z internetu. Mamy pewną losowość na starcie i zobaczmy czy się dostosuje. Zaczynamy od losowych kart na ręce i potrzebujemy zagrać 2 gry do 4 rundy. Zobaczmy czy się dostosuje.

Zakładamy sprint 2 tygodniowy. Należy też myśleć o prezentacji.


Z poprzedniego sprintu dalej implementowaliśmy kwestie wymyślania przez czaat xtrategi na kolejna runde rozgrywki aby mógł reflektowac tą strategie co runde 
Do tego z utrudnień dodaliśmy inna tallie kart na początek rozgrywki aby sprawdzić czy się dostosuje i nie miał on dużych dodatkowych problemów z innymi kartrami na start 
Oprócz tego aby urzóznowrodznicgre oraz zrobicja bardziej nie przewidywalnąi mniej schematyczna wprowadziliśmy eventy co runde które modyfikowały zminiały zasady  aby chat nie mógł korzystać z gotowej strategii internetowej i chat brał pod uwagę nasze zmoiany tepretycznie mocno tryzmałsieę wyznacoznej przez siebie strategii czylk mocnej bdowy ekonomi na poczatku co ejst ogólnie dobrym ząłożenim elcz stawerdzamy że czasem zbyt mocnio to znacyz analizowął on to że w jendej rudnzie jgo ruch jest gorszy ale jakby ułożył ona się juz od tą startegi e w ięc brbnał w to dalej i no nie próbwoałspojerzeć z innego kaa na sytuacje 
Jest on mocno nastawiony na maksymalizacje zyskó z każdej rudny zgodnie z sowjąstartegiaale czase kupuje akrty kte minimanie według nas bardziej rozżedzają talie niż są zyskie mlecz traktuj on to jako zysk 
uwązamy że nie licząc nadmiernego skupiania siena sowjej strategi wymysłonej na początku duza częśc rozumowanainia jest u niego poprawna potrafi analizowac posidane karty i ich ofekt aby wpłynąc sna sytuacje innych graczy bvrał też pod uwagę nei posdzieane eventy choc rzadk ozmusazłu one go do zmiany swopjeje strategii bo jej nie zaberaniały lecz conajmenj raz utrudniły lecz pozostał przy swoim 
NA tym etapie ai juzx rozumie potrzebe i wagte ppuktó zwycieśtwa i przynajmenj w rozumowaniu dążdy do ich zdobycia w rpzyszły h końćowo środkowych rudach tzn móimy tutaj w konteksie tych gier do 4 rundy gdyz bezposednio sprawdiztego nie mogliśmy ale  często otymn wpsominałtworzac starteghie
dostosowaywał sie też do weventó i po zabeventcie który blokuje wieksozśc optymalneych pól na plaszy stańał na najbardziej ekonomicznie opłaCALNYM polu i rozumie rónież wistonosć pól i to co które bardziej przynosi ekonomicznie 
 minusem może bcto za bardzo zaaangazownia sie w startegi co widac po ingporowaniu w tej fazie rozgrywki walk i skupoienieu sie na zasobach zi zdobywaniu pnktó zwycieśtwa poprzez zasoibvy chooc  w rozumowaniu twierdzi ze pózniej dostosje sie udało mu się utrymać na ty msamym poziomie putnkó zwyciestwa i podobnym poziomie zasobowo wpływowym coi nni gracze 
Część tygodnia poświeciliśmy na tworzenie prezentacji jesteśmy w trakcie tworzenia jej msuimy jeszcze dodać najnowsze przemyślenia i raporty oraz ogólne podsumowania projektu i nasze wnioski 



## **Raport z Podsumowania Sprintu 10: Testowanie Adaptacji i Odporności na Nieprzewidywalność**

Projekt: Mistrz Gry

### **1. Cel Sprintu**

Głównym celem Sprintu 10 była weryfikacja autentyczności procesów decyzyjnych AI. Chcieliśmy sprawdzić, czy model "Peter" faktycznie analizuje sytuację na bieżąco, czy jedynie powiela wyuczone schematy. Cel ten realizowaliśmy poprzez:

- **Losowość startową:** Rozpoczęcie gry z niestandardową talią kart oraz dodatkową, losową kartą Intrygi na ręce każdego gracza.
    
- **System Eventów:** Wprowadzenie co rundę modyfikatorów (blokady pól, zmiana kosztów, wymiana interesów).
    
- **Kontynuację Pamięci Strategicznej:** Utrzymanie mechanizmu refleksji strategicznej z poprzedniego sprintu.
    

### **2. Główne Wnioski z Testów (Analiza Adaptacji)**

#### **A. Reakcja na Eventy i Zmiany Pól**

Wprowadzone eventy modyfikowały dynamikę planszy:

1. **Blokowanie nietypowych pól:** Wyłączanie lokacji kluczowych dla standardowych strategii.
    
2. **Podnoszenie kosztów:** Zwiększanie ceny wejścia na konkretne pola.
    
3. **Wymiana interesów:** Tworzenie pól "droższych, ale zyskiwniejszych", oferujących większe korzyści za wyższą cenę.
    

**Wniosek:** AI reagowało na te zmiany poprawnie pod kątem logicznym. Peter rozumiał nowe koszty i ograniczenia, jednak jego reakcja była zachowawcza – model rzadko ryzykował, by skorzystać z "super-okazji" oferowanych przez eventy, wybierając bezpieczne ścieżki ekonomiczne.

#### **B. Problem "Betonowania" Strategii i "Lenistwa" AI**

Mechanizm strategii co rundę ujawnił specyficzną wadę modelu: **sztywność decyzyjną**.

- Nawet gdy eventy zmieniały sytuację na korzyść innej strategii, AI wykazywało tendencję do "trzymania się" pierwotnego planu.
    
- Zauważyliśmy pewne "lenistwo" w rewidowaniu założeń – jeśli sytuacja nie była tragiczna, model wolał brnąć w gorszy ruch zgodny z planem, zamiast wysilić się na stworzenie zupełnie nowej ścieżki.
    

#### **C. Enigma Kart Intryg – Problem Ignorancji**

W ramach zwiększania różnorodności, daliśmy każdemu graczowi (w tym AI) po jednej karcie Intrygi na start.

- **Obserwacja:** Mimo że otrzymana karta mogła stać się fundamentem stabilnej i silnej strategii, Peter praktycznie ją zignorował.
    
- **Wniosek:** Jest to problem powtarzający się od początku naszych rozgrywek. Choć model posiada kartę w danych (JSON), z niewyjaśnionych przyczyn nie włącza jej potencjału do swojego aktywnego planowania strategicznego, traktując ją jako element nieistniejący lub o zerowym priorytecie.
    

#### **D. Nadmierne skupienie na ekonomii**

Potwierdziliśmy, że AI jest zaprogramowane na "maksymalizację zysku surowcowego".

- **Zaleta:** Buduje potężny silnik ekonomiczny, dorównujący ludziom.
    
- **Wada:** Skupienie to jest tak silne, że model akceptuje "rozrzedzanie" talii słabymi kartami, jeśli tylko dają one jakikolwiek chwilowy zysk. Model traktuje każdą nową kartę jako sukces, nie rozumiejąc negatywnego wpływu zbyt dużej talii na statystykę dociągu.
    

### **3. Sukcesy i Progres Modelu**

Mimo zidentyfikowanych słabości, model wykazuje wysoką sprawność w:

- **Analizie stanu gry:** Precyzyjnie ocenia wpływ swoich ruchów na sytuację innych graczy.
    
- **Zrozumieniu celu:** W swoich przemyśleniach regularnie planuje zdobywanie Punktów Zwycięstwa (VP) w późniejszych fazach.
    
- **Dostosowaniu do blokad:** Gdy pole jest zablokowane, model bezbłędnie wybiera "drugą najlepszą" opcję ekonomiczną.
    