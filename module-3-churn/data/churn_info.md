# Telco Customer Churn — описание датасета

- Источник: https://www.kaggle.com/datasets/blastchar/telco-customer-churn
- Записей: 7043, признаков: 19 (+ customerID + Churn)
- Числовых: 3, категориальных: 16
- Классы: No — 5174 (73.5%), Yes — 1869 (26.5%)
- Пропуски: TotalCharges ~0.2% (пробелы), после pd.to_numeric → NaN, заполнено медианой