
---

# TODO: Aplikacja do przesyłania plików z Flask-WTF

## 1. Przygotowanie środowiska
- **Zainstaluj wymagane biblioteki**  
  W terminalu wykonaj polecenie:
  ```bash
  pip install Flask Flask-WTF python-dotenv
```

-  **Utwórz folder projektu**  
    Załóż nowy folder (np. `Twoj_Projekt`) i przejdź do niego.

## 2. Organizacja struktury projektu

-  **Utwórz strukturę folderów i plików**  
    Utwórz następującą strukturę:
    
    Twój Projekt
      ├── app/
      │   ├── templates/
      │   │   └── upload.html
      │   ├── __init__.py
      │   ├── forms.py
      │   └── routes.py
      ├── config.py
      └── .env
    
-  **Zadbaj o czytelność projektu**  
    Upewnij się, że każdy plik ma przypisaną odpowiedzialność – konfiguracja, inicjalizacja, logika tras i szablon.
    

## 3. Konfiguracja aplikacji (`config.py`)

-  **Utwórz plik `config.py`**
    
    - Zdefiniuj klasę konfiguracyjną z następującymi ustawieniami:
        
        - `SECRET_KEY` – pobierany z pliku `.env`
            
        - `UPLOAD_FOLDER` – folder, w którym będą zapisywane pliki
            
        - `ALLOWED_EXTENSIONS` – zbiór dozwolonych rozszerzeń (np. `{'txt', 'jpg'}`)
            
-  **Załaduj zmienne środowiskowe**  
    Użyj biblioteki `python-dotenv`, aby wczytać plik `.env`.
    

## 4. Inicjalizacja aplikacji (`__init__.py`)

-  **Utwórz plik `__init__.py` w folderze `app/`**
    
    - Zainicjalizuj aplikację Flask.
        
    - Załaduj konfigurację z pliku `config.py`.
        
    - Utwórz folder `UPLOAD_FOLDER` (jeśli nie istnieje) przy użyciu modułu `os`.
        
-  **Importuj moduł z trasami**  
    Zaimportuj plik `routes.py` na końcu, aby uniknąć problemów z cyklicznymi zależnościami.
    

## 5. Formularz przesyłania pliku (`forms.py`)

-  **Utwórz plik `forms.py` w folderze `app/`**
    
    - Zdefiniuj klasę formularza dziedziczącą po `FlaskForm`.
        
    - Dodaj pole `FileField` oraz przycisk `SubmitField`.
        
    - Upewnij się, że dodany jest validator `DataRequired`.
        

## 6. Szablon HTML (`upload.html`)

-  **Utwórz szablon w folderze `app/templates/`**
    
    - Stwórz prostą stronę HTML z formularzem przesyłania plików.
        
    - Wykorzystaj mechanizm CSRF (poprzez `form.hidden_tag()`).
        
    - Dodaj sekcję do wyświetlania komunikatów (np. przy użyciu `flash`).
        

## 7. Obsługa żądań (trasy) (`routes.py`)

-  **Utwórz plik `routes.py` w folderze `app/`**
    
    - Zdefiniuj trasę główną (np. `/`) obsługującą metody GET i POST.
        
    - Pobierz plik z formularza przy użyciu `form.file.data`.
        
    - Zabezpiecz nazwę pliku przy pomocy `secure_filename()` z biblioteki `werkzeug.utils`.
        
    - Zapisz plik w folderze określonym przez `UPLOAD_FOLDER`.
        
    - Użyj funkcji `flash` do wyświetlenia komunikatu o powodzeniu przesyłania.
        
    - Zaimplementuj przekierowanie po udanym przesłaniu pliku.
        

## 8. Konfiguracja środowiska (`.env`)

-  **Utwórz plik `.env`**
    
    - Dodaj zmienną `SECRET_KEY`, np.:
        SECRET_KEY = 'tajny-klucz-123!@#'

## 9. Uruchomienie aplikacji

-  **Uruchom serwer Flask**  
    W głównym folderze projektu wykonaj polecenie:
    
    ```bash
    flask run
    ```
    
-  **Sprawdź działanie aplikacji**  
    Otwórz przeglądarkę i przejdź do adresu [http://localhost:5000](http://localhost:5000/).
    

## 10. Testowanie funkcjonalności

-  **Przetestuj przesyłanie plików `.txt`**
    
    - Upewnij się, że po przesłaniu pliku, plik pojawia się w folderze `uploads`.
        
-  **Testuj walidację**
    
    - Spróbuj przesłać plik o rozszerzeniu innym niż `.txt` lub `.jpg` i sprawdź, czy walidacja działa poprawnie.
        
-  **Sprawdź komunikaty**
    
    - Upewnij się, że użytkownik otrzymuje komunikat o pomyślnym przesłaniu pliku.
        

## Rozszerzenia (opcjonalne)

-  **Obsługa plików JPG**  
    Rozszerz konfigurację `ALLOWED_EXTENSIONS`, aby obsługiwać także pliki `.jpg`.
    
-  **Ograniczenie rozmiaru pliku**  
    Dodaj mechanizm ograniczający maksymalny rozmiar przesyłanego pliku.
    
-  **Lista przesłanych plików**  
    Dodaj stronę wyświetlającą listę wszystkich przesłanych plików.
    
-  **Bezpieczeństwo przesyłania plików**  
    Rozważ dodatkowe zabezpieczenia przed przesyłaniem potencjalnie niebezpiecznych typów plików.
    
-  **Stylizacja formularza**  
    Dodaj arkusz CSS, aby poprawić wygląd formularza.
    

---

## Źródła pomocnicze

- [Dokumentacja Flask-WTF](https://flask-wtf.readthedocs.io/)
- [Bezpieczeństwo przesyłania plików w Flask](https://flask.palletsprojects.com/en/2.3.x/patterns/fileuploads/)
- [Obsługa środowiska w Flask (python-dotenv)](https://python-dotenv.readthedocs.io/)



---