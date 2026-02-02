# Predicting Student Test Scores - Kaggle Playground Series S6E1

**Autors:** Roksana Kanicka, Wiktoria Nowak
**Wynik CV:** RMSE 8.71058  

---

## Cel projektu

Przewidywanie wyników egzaminacyjnych studentów (0-100 punktów) na podstawie zmiennych opisujących styl nauki, warunki życiowe i zaangażowanie.

---

## Dane

- **Train:** 630,000 obserwacji
- **Test:** 270,000 obserwacji  
- **Original:** 20,000 obserwacji (źródło dla syntetycznych train/test)

Brak braków danych we wszystkich zbiorach.

---

## Explanatory Data Analysis

### Kluczowe wnioski:

1. **Rozkład zmiennej objaśnianej:**
   - Symetryczny rozkład exam_score (minimalna skośność ~0.06)
   - Train i original mają podobny rozkład

2. **Test ANOVA (p < 0.05):**
   - **Istotne:** sleep_quality, study_method, facility_rating
   - **Nieistotne (usunięte):** gender, course, internet_access, exam_difficulty

3. **Korelacje z exam_score:**
   - study_hours: 0.762
   - class_attendance: 0.361
   - sleep_hours: 0.167

4. **Profil studentów z wynikiem > 90%:**
   - study_hours: 6.7h (vs 3.8h reszta)
   - class_attendance: 80.8% (vs 69.1% reszta)
   - sleep_quality: 50% 'good'

---

## Feature Engineering

### 1. Ordinal Encoding
```python
sleep_quality: poor=1, average=2, good=3
facility_rating: low=1, medium=2, high=3
```

### 2. Wskaźniki
- **perfection_score:** suma warunków idealnych (study_hours ≥6.7, attendance ≥80.8%, sleep='good', method='coaching', facility='high')
- **struggle_score:** suma warunków trudnych (study_hours <1.7, attendance <68%, sleep_hours <6.5, sleep='poor')

### 3. Interakcje
- **engagement:** study_hours × (class_attendance/100)
- **study_efficiency:** study_hours × sleep_quality_ord
- **total_commitment:** study_hours + class_attendance/10

### 4. Agregaty z original dataset
Dla każdej zmiennej (study_hours, class_attendance, sleep_hours, study_method):
- `orig_mean_*`: średnia exam_score w grupach
- `orig_count_*`: liczebność grup


---

## Model

### XGBoost Regressor

**Parametry:**
```python
n_estimators: 2000
max_depth: 7
learning_rate: 0.01
random_state: 42
eval_metric: 'rmse'
```

**Walidacja:** 10-Fold Cross-Validation  
**Encoding:** Target encoding dla study_method

---

## Wyniki na train

| Metric | Value |
|--------|-------|
| CV RMSE | 8.71214 |
| Train size | 630,000 |
| Test size | 270,000 |
| Features | 20 |

### Top 5 Features (importance):
1. engagement (0.7019)
2. perfection_score (0.1183)
3. struggle_score (0.0563)
4. total_commitment (0.0310)
5. study_efficiency (0.0199)

### Wyniki na Kaggle
**Private Score:** 8.71058
**Public Score:** 8.68094

---

## Nieudane podejścia:
- overengineering
- LightGBM Ensemble (progres: 0.00016)
- bardzo restrykcyjne perfection_score progi
- dropowanie age


## Pliki

- `EDA_Predicting_Student_Test_Scores.py` - Eksploracyjna analiza danych
- `Przewidywanie_wyników_edukacyjnych.py` - Model XGBoost + submission
- `submission.csv` - Finalne predykcje (RMSE 8.704)

---

## Środowisko

```
Python 3.10
pandas 2.0.3
numpy 1.24.3
xgboost 2.0.3
scikit-learn 1.3.0
```

---

## Podsumowanie

Model XGBoost z zaprojektowanymi cechami (wskaźniki + agregaty + interakcje) osiągnął **Private Score:** 8.71058 (RMSE). Kluczowe decyzje były oparte na EDA (usunięcie nieistotnych cech, ordinal encoding) i klasycznych podejściach ML (target encoding, cross-validation). Osiągnęłbyśmy znacznie lepszy wynik na części danych, a po zakończeniu konkursu i pokazaniu wyniku na pełnych danych, niestety poszybowałyśmy na niższe miejsce.
