# 📉 Module 3 — Customer Churn: Ансамблевые методы

**Автор:** Коптяев Р.С., АСОиУб-23-2  
**Дата:** 2026-XX-XX

## 📊 Результаты

| Модель | Accuracy | Precision | Recall | F1 | ROC-AUC | Время |
|---|---|---|---|---|---|---|
| Random Forest | 0.78 | 0.64 | 0.73 | 0.68 | 0.83 | ~3 сек |
| XGBoost | 0.79 | 0.66 | 0.75 | 0.70 | 0.84 | ~2 сек |
| LightGBM | 0.80 | 0.67 | 0.76 | 0.71 | 0.84 | ~1 сек |
| CatBoost | 0.79 | 0.65 | 0.76 | 0.70 | 0.84 | ~5 сек |
| **LightGBM (Optuna)** | **0.81** | **0.70** | **0.76** | **0.73** | **0.86** | — |

## 🚀 Быстрый старт

```python
import joblib, requests
from io import BytesIO

BASE_URL = "https://raw.githubusercontent.com/KoptyaevRustam/ml-course-koptyaev/main/module-3-churn"
model = joblib.load(BytesIO(requests.get(f"{BASE_URL}/models/best_model.pkl").content))