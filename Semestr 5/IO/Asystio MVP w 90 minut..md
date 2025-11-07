Oto propozycja sformalizowanego planu projektu, uwzględniająca rozszerzony opis ról.

---

### Projekt: Prototyp Aplikacji Czatowej (MVP)

### 1. Kluczowe Wymagania (Kryteria MVP)

Minimalny zakres produktu (MVP) obejmuje następujące funkcjonalności:

1. Funkcjonująca aplikacja webowa realizująca funkcję czatu.
	
2. Zapis historii konwersacji (zapis ostatnich 10 wiadomości).
	
3. Implementacja funkcji zamiany mowy na tekst (Speech-to-Text, STT).
	

### 2. Stos Technologiczny

- **Backend:** Python, FastAPI, biblioteka `openai`.
	
- **Frontend:** React, `react-chat-elements`, `react-speech-recognition`.
	
	- _Uwaga:_ Przetwarzanie STT odbywa się w całości po stronie klienckiej (Frontend) i nie obciąża backendu.
		

### 3. Zespół i Podział Odpowiedzialności

- **Obszar Backendu:** Kacper Ślęzak, Kiryl Baranouski.
	
- **Obszar Frontendu:** Martyna Peukert, Tymon Woźniak.
	

Model Pracy:

Prace prowadzone są w dwóch równoległych zespołach (Backend i Frontend). 

### 4. Harmonogram Prac (Sesja 90-minutowa)

**Faza 1: Konfiguracja i Inicjalizacja (Minuty 0-15)**

- Utworzenie centralnego repozytorium kodu.
	
- Inicjalizacja projektu backendowego (FastAPI) oraz frontendowego (React).
	
- **Cel:** Osiągnięcie bazowego stanu "Hello World" dla obu części aplikacji, gotowych do dalszego rozwoju.
	

**Faza 2: Rozwój Równoległy (Minuty 15-50)**

- **Zespół Backend (Kacper, Kiryl):** Implementacja logiki biznesowej.
	
	- Stworzenie niezbędnych endpointów API (np. do wysyłania wiadomości, pobierania historii).
		
	- Integracja z API OpenAI.
		
	- Implementacja mechanizmu zapisu historii (np. do pliku JSON lub bazy danych in-memory).
		
- **Zespół Frontend (Martyna, Tymon):** Budowa interfejsu i logiki klienckiej.
	
	- Implementacja widoku czatu przy użyciu `react-chat-elements` na podstawie danych testowych (mocków).
		
	- Integracja i konfiguracja modułu STT (`react-speech-recognition`).
		
- _Założenie kluczowe:_ Oba zespoły pracują niezależnie, nie blokując się wzajemnie.
	

**Faza 3: Integracja Systemu (Minuty 50-80)**

- Krytyczny etap połączenia obu komponentów aplikacji.
	
- Zespół Frontend zastępuje dane testowe (mocki) rzeczywistymi wywołaniami do API backendowego.
	
- Przeprowadzenie pierwszych testów End-to-End (E2E) weryfikujących pełen przepływ danych (wprowadzenie tekstu/głosu -> wysłanie do API -> odpowiedź OpenAI -> wyświetlenie w UI).
	

**Faza 4: Weryfikacja i Bufor Czasowy (Minuty 80-90)**

- Zakończenie prac deweloperskich.
	
- Finalna weryfikacja działania aplikacji pod kątem zdefiniowanych kryteriów MVP (pkt. 1).
	
- Czas buforowy przeznaczony na ewentualne szybkie poprawki (hotfixy) lub debugowanie.
  
  
  AIzaSyB_ey238_F84hp-xa7FBltLWsP0iN4_LRk