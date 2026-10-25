# 🧹 Python Data Cleaning Practice

## 📌 Solution

## Prepare the data

```python
import pandas as pd

data = {
"name": [" Maria ", "Juan", "Maria ", "ANA", " Pedro", "Juan"],
"age": ["25", "30", "25", None, " 40", "30"],
"sex": ["Female", "male", "Female", "FEMALE", " Male ", "male"],
"income": ["25000", "30000", "25000", "35000", None, "30000"],
"date": ["2026-01-05", "2026/02/10", "2026-01-05", "2026-03-15", "invalid", "2026/02/10"]
}

```
## Clean and inspect the data
```python
#Inspect
print(pov_df.head)
print(pov_df.shape)
print(pov_df.columns)
pov_df.info()

#Check missing values
pov_df.isna()
pov_df.isna().sum()
pov_df.isnull()

#convert string to correct data type
pov_df['age'] = pd.to_numeric(pov_df['age'], errors='coerce')
pov_df['income'] = pd.to_numeric(pov_df['income'], errors='coerce')
pov_df['date'] = pd.to_datetime(pov_df['date'], errors='coerce')

#Handle missing values
#1 solution: use stat measurements to create assumptions - but not all the time, needs logical explanation why we are using mean to handle missing values
pov_df['age'] = pov_df['age'].fillna(pov_df['age'].mean())
pov_df['income'] = pov_df['income'].fillna(pov_df['income'].mean())
```

## Challenge: Missing reporting dates - Assumption: Missing reporting dates are assigned the Q1 2026, reporting timeline of March 31, 2026.
```python
pov_df['date'] = pov_df['date'].fillna(pd.Timestamp('2026-03-31'))

pov_df['age'] = pov_df['age'].astype(int)
pov_df['income'] = pov_df['income'].astype(int)

#Checking after changes
print(pov_df[['age', 'income','date']])
print(pov_df.head)
pov_df.info()

#Remove duplicates
duplicates = pov_df.duplicated()
print(duplicates)

#Handle duplicates
duplicates = pov_df.duplicated(subset=['age', 'income', 'date', 'name', 'sex'], keep=False)
pov_df[duplicates].sort_values(by = 'name')
pov_df.drop_duplicates(inplace = True)
print(pov_df.head)

#Clean the strings - do the cleaning first then remove the duplicate
pov_df['name'] = pov_df['name'].str.strip().str.capitalize()
pov_df['sex'] = pov_df['sex'].str.strip().str.capitalize()
#str.capitalize if just want the usual
pov_df.drop_duplicates(inplace=True)

#Verify
pov_df.info()
pov_df.isna().sum()
print(pov_df.duplicated().sum())
print(pov_df.head())

```
Answer: <img width="359" height="509" alt="image" src="https://github.com/user-attachments/assets/78822ea7-d6f6-4baf-b136-9b336191506d" />
