# Przewidywanie Jakości Powietrza – Projekt ML
### Informacje o projekcie
- **Przedmiot:** Uczenie Maszynowe 2025/2026
- **Kierunek:** Informatyka i ekonometria
- **Autorzy:** Roksana Kanicka, Wiktoria Nowak

## 1. Opis i cel projektu
Projekt opiera się na analizie danych z wielosensorowego urządzenia do pomiaru gazów, umieszczonego w silnie zanieczyszczonym obszarze włoskiego miasta. Dane obejmują roczny okres (marzec 2004 – luty 2005) i zawierają odpowiedzi z 5 czujników chemicznych na bazie tlenków metali.

**Główny cel:** Stworzenie i porównanie modeli regresyjnych, które w jak najlepszy sposób będą przewidywać zanieczyszczenie powietrza poprzez estymację stężenia tlenku węgla **CO(GT)**

## 2. Opis problemu do rozwiazania
Głównym wyzwaniem badawczym jest niska precyzja odczytów z tanich sensorów chemicznych (PT08.S1–PT08.S5). W przeciwieństwie do profesjonalnych, certyfikowanych analizatorów (GT – Ground Truth), tanie sensory są podatne na błędy wynikające z tzw. czułości krzyżowej (cross-sensitivity). Oznacza to, że ich odczyty są zniekształcone przez zmiany temperatury, wilgotności oraz obecność innych gazów (np. sensor CO może błędnie reagować na spaliny diesla).

Dodatkowo, zbiór danych posiada ograniczenia techniczne:
- **Braki danych:** Systemowe błędy oznaczone jako `-200`, wymagające preprocessingu.
- **Wielkość zbioru:** 9357 obserwacji godzinowych, co po usunięciu braków wymusza zastosowanie technik imputacji danych, aby zachować reprezentatywność zbioru.

## 3. Zbiór danych do treningu i testowania
- **Zbiór**: `Air Quality Data Set` z Kaggle
- **Link:** https://www.kaggle.com/datasets/fedesoriano/air-quality-data-set
- **Cechy (Features):**
  - `PT08.S1` - `PT08.S5`: Odpowiedzi tanich sensorów (tlenki metali) reagujących na różne składniki powietrza.
  - `T`, `RH`, `AH`: Parametry pogodowe (temperatura, wilgotność) służące do korekty błędów pomiarowych sensorów.
  - `Godzina`: Cecha wygenerowana z kolumny `Time`, uwzględniająca dobowe cykle zanieczyszczeń.
  - `Miesiąc`: Dla uwzględnienia sezonowości zanieczyszczeń.
- **Wartość przewidywana (Target)**
  - `CO(GT)`: Rzeczywiste stężenie tlenku węgla, które model ma oszacować.

## 4. Lista metod planowanych do zastosowania
W projekcie przetestujemy przynajmniej trzy podejścia regresyjne:

**1. Regresja Liniowa (Linear Regression)**

**2. Las Losowy (Random Forest Regressor)**

**3. XGBoost**

## 5. Miary oceny jakości modeli
Skuteczność modeli ocenimy za pomocą metryk:

- **MAE (Mean Absolute Error):** średni błąd bezwzględny
- **RMSE (Root Mean Squared Error):** pierwiastek błędu średniokwadratowego
- **$R^2$ (Współczynnik determinacji):** miara dopasowania modelu do danych

## 6. Planowany podział zadań
- **Roksana Kanicka:** Konfiguracja repozytorium, wczytanie danych, preprocessing, Eksploracyjna analiza danych (EDA), implementacja modeli Regresji Liniowej i XGBoost.
- **Wiktoria Nowak:** inżynieria cech (wyciągnięcie godziny), implementacja modelu Random Forest, implementacja alternatywnych modeli oraz końcowe porównanie wyników.

## 7. Do rozważenia:
- **Optymalizacja hiperparametrów** - wykorzystanie GridSearchCV do znalezienia najlepszych ustawień modeli.
- **Analiza ważności cech** -  Sprawdzenie, który sensor lub parametr pogodowy ma największy wpływ na błąd pomiarowy.
- **Analiza błędów (Error Analysis)**
