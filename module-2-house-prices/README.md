# Модуль 2 — House Prices: предобработка и регрессия

**Автор:** Коптяев Рустам Сергеевич, АСОиУб-23-2  
**Дисциплина:** Машинное обучение и искусственный интеллект  
**Дата сдачи:** 2026-11-03

## 📊 Результаты

В ходе работы были обучены 4 модели линейной регрессии с регуляризацией. Лучшей моделью признана **Lasso**, показавшая наилучший коэффициент детерминации (R²).

| Модель | RMSE (log) | MAE (log) | R² | RMSE ($) |
|---|---|---|---|---|
| Linear Regression | 0.135 | 0.095 | 0.88 | $28 000 |
| Ridge | 0.128 | 0.090 | 0.90 | $26 000 |
| **Lasso (best)** | **0.125** | **0.088** | **0.91** | **$25 000** |
| ElasticNet | 0.126 | 0.089 | 0.91 | $25 500 |

**Время обучения:** < 0.5 сек на каждую модель.  
**Ключевой инсайт:** `OverallQual` (общее качество) — сильнейший предиктор цены. Применение `log1p` к целевой переменной позволило поднять R² с 0.65 до 0.91.

## 🚀 Быстрый старт

Вы можете загрузить лучшую модель напрямую из репозитория, не переобучая её:

```python
import joblib
import requests
from io import BytesIO
import pandas as pd
import numpy as np

# Базовый URL для raw-файлов репозитория
BASE_URL = "https://raw.githubusercontent.com/KoptyaevRustam/ml-course-koptyaev/main/module-2-house-prices"

# Загрузка модели и scaler
model = joblib.load(BytesIO(requests.get(f"{BASE_URL}/models/best_model.pkl").content))
scaler = joblib.load(BytesIO(requests.get(f"{BASE_URL}/models/scaler.pkl").content))
feature_cols = requests.get(f"{BASE_URL}/models/feature_cols.json").json()
