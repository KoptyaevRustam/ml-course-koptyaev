# 📊 Описание датасета: Online Shoppers Purchasing Intention

## 🔗 Источник данных

| Параметр | Значение |
|---|---|
| **Название** | Online Shoppers Purchasing Intention Dataset |
| **Оригинал** | [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Online+Shoppers+Purchasing+Intention+Dataset) |
| **Зеркало** | [Kaggle — roshansharma](https://www.kaggle.com/datasets/roshansharma/online-shoppers-intention) |
| **Авторы** | C. Okan Sakar, S. Olcay Polat, Mete Gürsoy |
| **Год** | 2018–2019 |
| **Публикация** | Sakar et al. (2019). Real-time prediction of online shoppers' purchasing intention using multilayer perceptron and LSTM recurrent neural networks. *Neural Computing and Applications*, 31, 6893–6908. |
| **Лицензия** | CC BY 4.0 |
| **Файл в репозитории** | `module-4-features/data/online_shoppers_intention.csv` |

---

## 📐 Общая структура

| Параметр | Значение |
|---|---|
| **Всего записей** | 12 330 |
| **Признаков (входных)** | 17 |
| **Целевая переменная** | 1 (`Revenue`) |
| **Всего столбцов** | 18 |
| **Тип задачи** | Бинарная классификация |
| **Пропуски** | 0 (все столбцы заполнены) |
| **Дубликаты** | 0 |
| **Классов** | 2 |

### Разбиение на выборки (в ноутбуке)

| Выборка | Доля | Записей |
|---|---|---|
| Train | 80% | 9 864 |
| Test | 20% | 2 466 |
| **Стратификация** | `stratify=y` | ✅ сохранены доли классов |

---

## 🎯 Целевая переменная: `Revenue`

| Значение | Класс | Количество | Доля |
|---|---|---|---|
| `False` | Нет покупки | 10 422 | **84.5%** |
| `True` | Покупка | 1 908 | **15.5%** |

**Дисбаланс:** 84.5 / 15.5 ≈ **5.4:1** — сильный.

**Последствия для моделирования:**
- Accuracy **не подходит** как основная метрика (модель «всегда False» даст 0.845).
- Используются:
  - `class_weight='balanced'` (RF, LightGBM);
  - `scale_pos_weight ≈ 5.4` (XGBoost);
  - `auto_class_weights='Balanced'` (CatBoost);
  - **ROC-AUC** как основная метрика;
  - **F1-score**, **Recall** — как вспомогательные.

---

## 📋 Описание всех столбцов

### Числовые признаки поведения (10 шт.)

| # | Столбец | Тип | Диапазон | Описание |
|---|---|---|---|---|
| 1 | `Administrative` | int | 0–27 | Число посещённых административных страниц |
| 2 | `Administrative_Duration` | float | 0–3398 | Время на административных страницах (сек) |
| 3 | `Informational` | int | 0–24 | Число информационных страниц |
| 4 | `Informational_Duration` | float | 0–2549 | Время на информационных страницах (сек) |
| 5 | `ProductRelated` | int | 0–705 | Число товарных страниц |
| 6 | `ProductRelated_Duration` | float | 0–63 973 | Время на товарных страницах (сек) |
| 7 | `BounceRates` | float | 0–0.20 | Средний показатель отказов по страницам сессии |
| 8 | `ExitRates` | float | 0–0.20 | Средний показатель выходов по страницам сессии |
| 9 | `PageValues` | float | 0–361.76 | Средняя ценность страницы (по данным Google Analytics) |
| 10 | `SpecialDay` | float | 0–1.0 | Близость сессии к празднику (0 = будний день, 1 = праздник) |

### Категориальные / дискретные признаки (6 шт.)

| # | Столбец | Тип | Уникальных | Описание |
|---|---|---|---|---|
| 11 | `Month` | object | 10 | Месяц сессии: `Feb, Mar, May, June, Jul, Aug, Sep, Oct, Nov, Dec` |
| 12 | `OperatingSystems` | int | 8 | ОС пользователя (закодирована, расшифровки в датасете нет) |
| 13 | `Browser` | int | 13 | Браузер (закодирован) |
| 14 | `Region` | int | 9 | Регион (закодирован) |
| 15 | `TrafficType` | int | 20 | Тип трафика (закодирован) |
| 16 | `VisitorType` | object | 3 | `New_Visitor`, `Returning_Visitor`, `Other` |
| 17 | `Weekend` | bool | 2 | `True` — выходной, `False` — будний |

### Целевая (1 шт.)

| # | Столбец | Тип | Описание |
|---|---|---|---|
| 18 | **`Revenue`** | bool | `True` = сессия завершилась покупкой |

> **Примечание:** коды `OperatingSystems`, `Browser`, `Region`, `TrafficType` в исходном датасете **анонимизированы** — оригинальные значения (например, «Windows», «Chrome», «Europe») в публичной версии не раскрываются.

---

## 📈 Статистика числовых признаков

| Признак | Mean | Std | Min | 25% | 50% | 75% | Max |
|---|---|---|---|---|---|---|---|
| `Administrative` | 2.32 | 3.32 | 0 | 0 | 1 | 4 | 27 |
| `Administrative_Duration` | 80.82 | 176.70 | 0 | 0 | 7.5 | 93.3 | 3398 |
| `Informational` | 0.50 | 1.27 | 0 | 0 | 0 | 0 | 24 |
| `Informational_Duration` | 34.47 | 140.75 | 0 | 0 | 0 | 0 | 2549 |
| `ProductRelated` | 31.73 | 44.53 | 0 | 7 | 18 | 38 | 705 |
| `ProductRelated_Duration` | 1194.75 | 1913.98 | 0 | 183.6 | 598.9 | 1464.2 | 63 973 |
| `BounceRates` | 0.022 | 0.048 | 0 | 0.003 | 0.003 | 0.016 | 0.20 |
| `ExitRates` | 0.043 | 0.048 | 0 | 0.014 | 0.025 | 0.050 | 0.20 |
| `PageValues` | 5.89 | 18.51 | 0 | 0 | 0 | 0 | 361.76 |
| `SpecialDay` | 0.062 | 0.20 | 0 | 0 | 0 | 0 | 1.0 |

**Наблюдения:**
- `PageValues` имеет **медиану 0** и огромный правый хвост — сильно скошено (skew ≈ 7). Большинство сессий — без ценности страницы.
- `ProductRelated_Duration` тоже скошено (skew ≈ 8.5) — стоит логарифмировать при использовании в линейных моделях.
- `BounceRates` и `ExitRates` сильно коррелированы (r ≈ 0.91) — мультиколлинеарность (важно для линейных моделей, для деревьев некритично).

---

## 📊 Распределение категориальных признаков

### `Month`

| Месяц | Кол-во | Доля покупок |
|---|---|---|
| Feb | 184 | 1.6% |
| Mar | 1 907 | 10.2% |
| May | 1 665 | 10.4% |
| June | 361 | 10.5% |
| Jul | 432 | 12.5% |
| Aug | 433 | 13.6% |
| Sep | 448 | 12.9% |
| Oct | 549 | 20.9% |
| **Nov** | **2 998** | **25.4%** ← пик (Black Friday) |
| Dec | 1 727 | 12.5% |

**Пик:** ноябрь (25.4% покупок), **минимум:** февраль (1.6%).

### `VisitorType`

| Тип | Кол-во | Доля покупок |
|---|---|---|
| `Returning_Visitor` | 10 551 | ~14% |
| `New_Visitor` | 1 704 | ~10% |
| `Other` | 75 | ~14% |

**Возвращающиеся покупают чаще новых** — важный сигнал для бизнес-воронки.

### `Weekend`

| Значение | Кол-во |
|---|---|
| `False` (будни) | 9 467 |
| `True` (выходные) | 2 863 |

Покупки в выходные **незначительно чаще** (≈17% vs ≈15%).

---

## 🔧 Инженерные признаки (созданы в ноутбуке)

| Признак | Формула | Тип | Обоснование |
|---|---|---|---|
| `TotalPages` | `Administrative + Informational + ProductRelated` | int | Глубина просмотра — интегральный сигнал вовлечённости |
| `TotalDuration` | сумма всех `*_Duration` | float | Общее время на сайте — ключевой сигнал «горячего» пользователя |
| `AvgPageValue` | `PageValues / (TotalPages + 1)` | float | Средняя ценность страницы (нормализована на глубину) |
| `AvgTimePerPage` | `TotalDuration / (TotalPages + 1)` | float | Время на страницу — «залипание» |
| `ProductRatio` | `ProductRelated / (TotalPages + 1)` | float | Доля товарных страниц — фокус на покупке |
| `BounceExitRatio` | `BounceRates / (ExitRates + 0.001)` | float | Соотношение отказов и выходов |
| `MonthNum` | Feb→2, Mar→3, …, Dec→12 | int | Числовой месяц для учёта сезонности |
| `IsNewVisitor` | `VisitorType == 'New_Visitor'` | 0/1 | Флаг нового посетителя |
| `IsWeekend` | `Weekend` (bool → int) | 0/1 | Выходной ли день |
| `IsHighTraffic` | `TrafficType > 10` | 0/1 | Высокий трафик |
| `IsHighSeason` | `MonthNum ∈ {5, 11, 12}` | 0/1 | Пиковые месяцы (May, Nov, Dec) |
| `PageValue_Duration` | `PageValues × TotalDuration` | float | Взаимодействие: ценность × время |
| `ProductValue` | `PageValues × ProductRelated` | float | Взаимодействие: ценность × товарные страницы |

**Защита от деления на ноль:** везде `+ 1` в знаменателе (или `+ 0.001` для отношений).
**One-Hot для `VisitorType`:** `VT_New_Visitor`, `VT_Returning_Visitor`, `VT_Other` (drop_first=False, чтобы сохранить все 3 категории).

---

## 🧠 Ключевые инсайты по данным

1. **`PageValues` — сильнейший предиктор.** Если `PageValues > 0` — вероятность покупки резко возрастает. Медиана 0 у непокупателей vs заметные значения у покупателей.
2. **`TotalDuration` и `ProductRelated_Duration`** — вторые по важности. Длительные сессии с высокой долей товарных страниц = «горячий» клиент.
3. **`ExitRates` / `BounceRates`** — негативные предикторы. Высокие значения = уход без покупки.
4. **`MonthNum = 11` (ноябрь)** — положительный вклад (Black Friday).
5. **`IsNewVisitor = 1`** — отрицательный вклад (новые покупают реже).
6. **`TrafficType`** — некоторые типы трафика (например, type 8) дают заметно более высокую конверсию.

---

## 🧪 Как воспроизвести анализ

```python
import pandas as pd

df = pd.read_csv('data/online_shoppers_intention.csv')

print(df.shape)                    # (12330, 18)
print(df['Revenue'].value_counts())  # False: 10422, True: 1908
print(df.isnull().sum().sum())     # 0 — пропусков нет
print(df.describe().round(2))
```

Полный EDA — в `notebook.ipynb`, раздел 5 (ячейки с визуализациями и Feature Engineering).

---

## 📁 Связанные файлы в репозитории

| Файл | Что внутри |
|---|---|
| `data/online_shoppers_intention.csv` | Исходные данные (12 330 × 18) |
| `data/dataset_info.md` | ← этот файл |
| `notebook.ipynb` | Полный EDA + моделирование + SHAP |
| `models/feature_cols.json` | Список финальных признаков (порядок важен для модели!) |
| `models/metrics.json` | Метрики всех 4 моделей + параметры Optuna |
| `examples/eda_plots.png` | 6 EDA-графиков |

---

## ⚠️ Ограничения и замечания

1. **Анонимизация категориальных признаков** (`OperatingSystems`, `Browser`, `Region`, `TrafficType`) — нельзя интерпретировать коды без внешнего словаря.
2. **Датасет — снимок 2018–2019 гг.** Поведение пользователей и сезонность могли измениться (пост-COVID, mobile-first, cookie-less tracking).
3. **Дисбаланс 84.5 / 15.5** — сильный; без `class_weight` или SMOTE модель «скатится» к мажоритарному классу.
4. **Мультиколлинеарность** `BounceRates` ↔ `ExitRates` — для линейных моделей нужна регуляризация (L2/ElasticNet), для деревьев некритично.
5. **Выбросы в `ProductRelated_Duration`** (до 63 973 сек ≈ 17.8 часов) — вероятно, боты или оставленные вкладки; рассмотреть обрезку по 99-му перцентилю.

---

## 📚 Источники

1. Sakar, C.O., Polat, S.O., Katircioglu, M., Kastro, Y. (2019). Real-time prediction of online shoppers' purchasing intention using multilayer perceptron and LSTM recurrent neural networks. *Neural Computing and Applications*, 31, 6893–6908.
2. UCI ML Repository: https://archive.ics.uci.edu/ml/datasets/Online+Shoppers+Purchasing+Intention+Dataset
3. Kaggle: https://www.kaggle.com/datasets/roshansharma/online-shoppers-intention