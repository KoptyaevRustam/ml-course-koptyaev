# Модуль 1 — Titanic: EDA + бинарная классификация

**Автор:** Коптяев Рустам Сергеевич, АСОиУб-23-2  
**Дата:** 2026-09-29

## 📊 Результаты

| Модель | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---|---|---|---|---|
| Logistic Regression | 0.8212 | 0.7937 | 0.7246 | 0.7576 | 0.8572 |
| Decision Tree | 0.7654 | 0.7077 | 0.6667 | 0.6866 | 0.8014 |

**Время обучения:** LR — 0.0055 сек, DT — 0.0030 сек

## 🚀 Быстрый старт

```python
import joblib, requests
from io import BytesIO
BASE_URL = "https://raw.githubusercontent.com/koptyaev-rs/ml-course-koptyaev/main/module-1-titanic"
model = joblib.load(BytesIO(requests.get(f"{BASE_URL}/models/lr_model.pkl").content))
