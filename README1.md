# 🛃 Customer Spending and EDA

## 📌 Solution

## Data Quality

```python
import pandas as pd
import numpy as np

eda = pd.read_csv("C:/Users/USER/Downloads/archive/EDA_Practice_Dataset.csv")

#Step 2 - Inspect
print(eda.head)
print(eda.shape)
print(eda.columns)
eda.info()

#Step 3 — Check missing values and Missing-value percentage
print(eda.isna().sum())
print(eda.isna().mean() * 100)
print((eda.isna().mean() * 100).round(2))

#Step 4 - Let's check for duplicate rows.
print(eda.duplicated().sum())

#Step 5 - Inspect the duplicates
print(eda[eda.duplicated()])

#Step 6 - Inspect the full duplicate pairs
print(eda[eda.duplicated(keep=False)].sort_values("Customer_ID"))

#Step 7 - Convert the date column
eda["Purchase_Date"] = pd.to_datetime(
    eda["Purchase_Date"],
    errors="coerce"
)

print(eda["Purchase_Date"].dtype)
print(eda.dtypes)

#Step 8 - Summarize Stats
print(eda["Purchase_Date"].min())
print(eda["Purchase_Date"].max())

#Step 9 - Numerical overview
print(eda.describe())

#Step 10 - non-numerical categorical variables
print(eda["Gender"].value_counts(dropna=False))
print(eda["City"].value_counts(dropna=False))
print(eda["Is_Member"].value_counts(dropna=False))

```
## Data Analysis

# Question 1: Find all customers whose Age is 40 or older.
```python
print(eda[eda["Age"] >= 40])



