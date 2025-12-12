### Raport z analizy podatności (CTF)

**1. flag={png_flag_coll3cted} (Obrazek)**

- **Typ podatności:** Information Leakage (Wyciek metadanych).
    
- **Analiza:** Pliki graficzne mogą zawierać metadane (EXIF), które nie są widoczne podczas standardowego wyświetlania obrazu. Przeprowadzono analizę pliku `blog_girl.png` przy użyciu narzędzia `exiftool`. Flaga została zidentyfikowana w polu komentarza (Comment) wewnątrz metadanych pliku.
    

**2. flag={mission_accompli9hed} (Administrator)**

- **Typ podatności:** Insecure Direct Object Reference (IDOR).
    
- **Analiza:** Mechanizm autoryzacji opierał się wyłącznie na walidacji parametru w adresie URL, bez weryfikacji sesji po stronie serwera. Zmiana wartości parametru `user` w zapytaniu GET (z domyślnej na `?user=administrator`) pozwoliła na obejście zabezpieczeń i uzyskanie dostępu do panelu administracyjnego.
    

**3. flag={g0t_ya} (Admin Admin)**

- **Typ podatności:** Default Credentials.
    
- **Analiza:** Panel logowania administratora był zabezpieczony domyślnymi danymi uwierzytelniającymi (`admin` / `admin`). Wykorzystanie tych powszechnie znanych poświadczeń umożliwiło zalogowanie się do systemu, gdzie flaga była widoczna bezpośrednio w interfejsie.


**4. flag={k1nda_sus} (Article 31)**

- **Typ podatności:** Broken Access Control.

- **Analiza:** Zasób (artykuł nr 31) został ukryty poprzez brak bezpośredniego linkowania w menu (Security by Obscurity), jednak nie posiadał mechanizmu kontroli dostępu. Manipulacja parametrem ID w adresie URL (`search=31`) wymusiła na serwerze wyświetlenie ukrytej treści.


**5. flag={great_m8} (Upload)**

- **Typ podatności:** File Upload Vulnerability / Improper Error Handling.

- **Analiza:** System weryfikacji plików odrzucał pliki o nieprawidłowym rozszerzeniu, ale zwracał przy tym nadmiernie szczegółowe komunikaty błędów (verbose errors). Próba przesłania pliku innego niż obraz (np. `.txt`) spowodowała wyświetlenie wyjątku systemowego, w treści którego ujawniono flagę.


**6. flag={2_easy} (SQL Injection)**

- **Typ podatności:** SQL Injection (SQLi) – Union Based.

- **Analiza:** Pole wyszukiwania nie przeprowadzało sanityzacji danych wejściowych. Wykorzystano operator `UNION SELECT` do wstrzyknięcia własnego zapytania SQL. Pozwoliło to na odczytanie zawartości tabeli `users` i wydobycie hasła dla użytkownika `secret`, które stanowiło flagę.


**7. flag={hey_h4cker} (Źródło strony)**

- **Typ podatności:** Sensitive Data Exposure (Client-side code).

- **Analiza:** Przeprowadzono inspekcję kodu źródłowego strony (HTML). Flaga została odnaleziona wewnątrz komentarza HTML (``). Dane te nie są renderowane przez przeglądarkę, ale są w pełni dostępne dla każdego użytkownika po wyświetleniu źródła strony.


**8. flag={7azy_flag} (Article 1 - Base64)**

- **Typ podatności:** Weak Encoding.

- **Analiza:** W treści artykułu zidentyfikowano ciąg znaków zakodowany w formacie Base64. Base64 jest metodą kodowania (encoding), a nie szyfrowania, co oznacza, że jest łatwo odwracalny. Zdekodowanie ciągu ujawniło ukrytą treść flagi.


**9. flag={JWT_Token5} (Article 2 - JWT)**

- **Typ podatności:** Information Disclosure (JWT).

- **Analiza:** Przechwycono przykładowy token JWT (JSON Web Token). Tokeny te nie są domyślnie szyfrowane, a jedynie zakodowane (Base64Url). Po zdekodowaniu sekcji Payload (np. przy użyciu debugera JWT), odczytano flagę zapisaną jawnym tekstem w strukturze JSON tokena.


**10. flag={6@@D-job} (XXE)**

- **Typ podatności:** XML External Entity (XXE) Injection.

- **Analiza:** Parser XML aplikacji posiadał włączoną obsługę zewnętrznych encji (`resolve_entities=True`). Wykorzystano tę podatność, przesyłając spreparowany payload XML definiujący encję zewnętrzną wskazującą na plik `/flag.txt`. Serwer przetworzył encję i zwrócił zawartość lokalnego pliku w odpowiedzi aplikacji.
