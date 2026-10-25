<img width="460" height="320" alt="image" src="https://github.com/user-attachments/assets/8f2ff42b-a8e4-4a89-90aa-5346bc14d936" /># 🛃 Customer Spending and EDA

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

## Question 1: Find all customers whose Age is 40 or older.
```python
print(eda[eda["Age"] >= 40])
```
Answer: <img width="635" height="365" alt="image" src="https://github.com/user-attachments/assets/c5f614e3-dd48-40ae-9b3b-9395429f66cd" />

## Question 2: Find customers who are 40 or older AND have a salary greater than 3,000.
```python
print(eda[(eda["Age"] >= 40) & (eda["Salary"] > 3000)])
```
Answer: <img width="630" height="421" alt="image" src="https://github.com/user-attachments/assets/55fb5e00-391d-410e-b826-b3dabd8f9bc2" />

## Question 3: Show only Customer_ID, Age, Salary, and City
```python
print(eda[["Customer_ID", "Age", "Salary", "City"]])
```
Answer: <img width="460" height="320" alt="image" src="https://github.com/user-attachments/assets/b819965d-7d5e-47b7-aaf7-baa1e87763f5" />

## Question 4: Show only Customer_ID, Age, Salary, and City for customers whose Salary is greater than 3,000.
```python
print(eda.loc[eda["Salary"] > 3000, ["Customer_ID", "Age", "Salary", "City"]])
print(
    eda[eda["Salary"] > 3000][
        ["Customer_ID", "Age", "Salary", "City"]
    ]
)
```
Answer: <img width="350" height="304" alt="image" src="https://github.com/user-attachments/assets/1b8758e6-58cc-4038-9126-3d079dae712f" />

## Question 5: Create a new column called spending_rate that shows what percentage of each customer's salary they spent.
```python
eda["spending_rate"] = (100 * eda["Purchase_Amount"] / eda["Salary"]).round(2)
print(eda[["Customer_ID", "Salary", "Purchase_Amount", "spending_rate"]])

#Summarize
print(eda["spending_rate"].mean().round(2))

#Group + Summarize - What is the average spending rate for each city?
print(eda.groupby("City")["spending_rate"].mean().round(2))

#Sort the grouped result - Sort the average spending rate from highest to lowest city.
print(
    eda.groupby("City")["spending_rate"]
    .mean()
    .round(2)
    .sort_values(ascending=False)
)
```
Answer: <img width="494" height="278" alt="image" src="https://github.com/user-attachments/assets/99ebd8e4-02a4-40c0-9cc2-35d40bc0a426" /> 
<img width="399" height="272" alt="image" src="https://github.com/user-attachments/assets/90ca4fa3-18d5-4f3a-8436-e00c43ac1b4e" />

## Question 6: Among customers who are members (Is_Member == "Yes"), what is the average Purchase_Amount for each city?
```python
print(
    eda[eda["Is_Member"] == "Yes"]
    .groupby("City")["Purchase_Amount"]
    .mean()
    .round(2)
)
# What is the average Purchase_Amount for Is_Member == "Yes" versus Is_Member == "No"
print(
    eda.groupby("Is_Member")["Purchase_Amount"]
    .mean()
    .round(2)
)

# #Which city has the highest average salary?
print(
    eda.groupby("City")["Salary"]
    .mean()
    .round(2)
    .sort_values(ascending=False)
)

#Is there a relationship between Salary and Purchase_Amount?
print(eda["Salary"].corr(eda["Purchase_Amount"]).round(2))
```
Answer: <img width="375" height="257" alt="image" src="https://github.com/user-attachments/assets/a31a97a9-d796-480b-b4ff-5a629884cb93" />
<img width="721" height="216" alt="image" src="https://github.com/user-attachments/assets/49d2a697-3970-4b40-a1a5-2e082288f1fa" />
<img width="413" height="291" alt="image" src="https://github.com/user-attachments/assets/452a4ade-e1c3-4a6b-8998-c4b983870c94" />
<img width="534" height="61" alt="image" src="https://github.com/user-attachments/assets/6e96cf2a-af8c-4e23-89ad-2a5f1469c31e" />
- Correlation between Salary and Purchase_Amount?: A correlation of 0.01 means almost no linear relationship between Salary and Purchase_Amount.

## Question 7: What is the average Purchase_Amount for customers aged 40 and above versus customers under 40?
```python
eda["age_group"] = np.select(
    [
        eda["Age"].isna(),
        eda["Age"] >= 40
    ],
    [
        "Missing",
        "40+"
    ],
    default="Under 40"
)
print(eda[["Age", "age_group"]])
print(eda["age_group"].value_counts(dropna=False))
print(eda["age_group"].value_counts())

print(
    eda[eda["age_group"] != "Missing"]
    .groupby("age_group")["Purchase_Amount"]
    .mean()
    .round(2)
)
```
Answer: <img width="323" height="306" alt="image" src="https://github.com/user-attachments/assets/c50b7972-7379-4b01-92f4-efd51207377c" />

## Question 8: For each city, calculate the average Purchase_Amount for members only (Is_Member == "Yes"), then sort from highest to lowest.

```python
print(
    eda[eda["Is_Member"] == "Yes"]
    .groupby("City")["Purchase_Amount"]
    .mean()
    .round(2)
    .sort_values(ascending=False)
)
```
Answer: <img width="395" height="290" alt="image" src="https://github.com/user-attachments/assets/e1edae0b-39cd-45b2-bf38-a60ff6ce7330" />







