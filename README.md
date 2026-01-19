# Optymalizacja modeli regresyjnych w przewidywaniu wyników edukacyjnych: Udział w konkursie Kaggle S6E1.
### Informacje o projekcie
- **Przedmiot:** Uczenie Maszynowe 2025/2026
- **Kierunek:** Informatyka i ekonometria
- **Autorzy:** Roksana Kanicka, Wiktoria Nowak

## 1. Opis i cel projektu
Celem projektu jest stworzenie modelu uczenia maszynowego, który na podstawie danych demograficznych i akademickich precyzyjnie przewidzi wynik egzaminu studenta. Prace zostaną podzielone na cztery główne etapy. Pierwszym krokiem będzie eksploracyjna analiza danych (EDA), mająca na celu identyfikację korelacji między cechami (np. godzinami nauki, frekwencją) a zmienną celu (exam_score) oraz wykrycie ewentualnych anomalii w syntetycznym zbiorze danych.

**Główny cel:** Porównanie wyników z rankingiem na platformie Kaggle

## 2. Zbiór danych do treningu i testowania
Zbiór danych pochodzi z konkursu Kaggle Predicting Student Test Scores. Składa się z pliku train.csv (dane treningowe z etykietami) oraz test.csv (dane do predykcji konkursowej).
https://www.kaggle.com/competitions/playground-series-s6e1

## 3. Lista metod planowanych do zastosowania
    Modele: Linear Regression (baseline), Random Forest, XGBoost, LightGBM, CatBoost.

    Techniki: K-Fold Cross-Validation, Optuna (hyperparameter tuning), Weighted Averaging/Stacking (ensembling).

    Narzędzia: Python (Scikit-learn, Pandas, NumPy), WandB, Kaggle API.

## 4. Miary oceny jakości modeli
Główną miarą oceny, zgodnie z wymaganiami konkursu, będzie RMSE (Root Mean Squared Error). Dodatkowo będziemy monitorować współczynnik determinacji R2, aby ocenić, jaki procent wariancji zmiennej celu wyjaśnia nasz model.

## 5. Planowany podział zadań
- **Roksana Kanicka:** Implementacja modeli bazowych i zaawansowanych (XGBoost, LightGBM, CatBoost), optymalizacja hiperparametrów (Optuna), przygotowanie finalnej submisji.
- **Wiktoria Nowak:** Eksploracyjna analiza danych (EDA), inżynieria cech (feature engineering), integracja z platformą Weights & Biases (wandb.com).
