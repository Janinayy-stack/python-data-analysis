# 📈 Customer Spending Analysis and Visualization

## 📌 Solution

## Data Inspection

```python
import pandas as pd
import numpy as np

eda_viz = pd.read_csv(r"C:\Users\USER\Downloads\Data Analysis apps\eda_faci.csv")

#Part A — Data Inspection
print(eda_viz.head)
print(eda_viz.shape)
print(eda_viz.columns)
eda_viz.info()
eda_viz.describe()

#Check missing values and Missing-value percentage, duplicated rows
print(eda_viz.isna().sum())
print(eda_viz.isna().mean() * 100)
print((eda_viz.isna().mean() * 100).round(2))
print(eda_viz.duplicated().sum())
print(eda_viz[eda_viz.duplicated()])
print(eda_viz[eda_viz.duplicated(keep=False)].sort_values("Customer_ID"))

#Part B — EDA Basic summaries
print("Average age:", round(eda_viz["Age"].mean(), 2))#round then average
print("Average Purchase Amount:", round(eda_viz["Purchase_Amount"].mean(), 2))
print("Total Salary:", round(eda_viz["Salary"].sum(), 2))
print(eda_viz["Is_Member"].value_counts())
```
Answer: <img width="286" height="153" alt="image" src="https://github.com/user-attachments/assets/704d3c56-d555-4778-ba72-4d667cedc918" />

## Data Analysis
-  City Analysis Summaries
```python
print(eda_viz.groupby("City")["Customer_ID"]
    .count()
)
print(round(eda_viz.groupby("City")["Salary"].mean().sort_values(ascending=False), 2))
print(round(eda_viz.groupby("City")["Purchase_Amount"].mean().sort_values(ascending=False), 2))
print(eda_viz.groupby("City")["Purchase_Amount"].sum().sort_values(ascending=False))
```
Answer: <img width="350" height="540" alt="image" src="https://github.com/user-attachments/assets/9816c28b-3340-43e3-b02e-e562d72d8bb9" />

- Members Analysis Summaries
```python
print(eda_viz.groupby("Is_Member")["Customer_ID"]
    .count()
)
print(round(eda_viz.groupby("Is_Member")["Salary"].mean().sort_values(ascending=False), 2))
print(round(eda_viz.groupby("Is_Member")["Purchase_Amount"].mean().sort_values(ascending=False), 2))
```
Answer: <img width="327" height="262" alt="image" src="https://github.com/user-attachments/assets/da64bf95-cd54-4c11-8fca-5a08b5289303" />

## Visualization
- Bar chart - Total purchase amount by city
```python
import matplotlib.pyplot as plt

city_purchases = (
    eda_viz.groupby("City")["Purchase_Amount"]
    .sum()
    .sort_values(ascending=False)
)

fig, ax = plt.subplots()
ax.bar(city_purchases.index, city_purchases.values)
ax.set_xticks(range(len(city_purchases.index))) #Set locations first, THEN set the labels
ax.set_xticklabels(city_purchases.index, rotation=90)

ax.set_ylabel("Total Purchase Amount")
ax.set_title("Total Purchase Amount by City")
plt.tight_layout()
plt.show()

```
Answer: <img width="628" height="560" alt="image" src="https://github.com/user-attachments/assets/3532a6a2-87c1-477e-b66a-015d55a8f1f8" />

- Average purchase amount of members vs non-members
```python
is_member_purchases = (eda_viz.groupby("Is_Member")["Purchase_Amount"]
    .mean()
    .sort_values(ascending=False)
)

fig, ax = plt.subplots()
ax.bar(is_member_purchases.index, is_member_purchases.values)
ax.set_xticks(range(len(is_member_purchases.index)))
ax.set_xticklabels(is_member_purchases.index, rotation=90)

ax.set_ylabel("Average Purchase Amount")
ax.set_title("Average Purchase Amount by Member Status")
plt.tight_layout()
plt.show()
```
Answer: <img width="632" height="551" alt="image" src="https://github.com/user-attachments/assets/38d2d7f1-e543-4b0d-885d-b3560b1a8c11" />

- Line or ordered chart - Average Purchase Amount by Age
```python
eda_viz.groupby("Age")["Purchase_Amount"].mean().plot(
    kind="line",
    marker="o",
    title="Average Purchase Amount by Age",
    ylabel="Average Purchase"
)
plt.show()
```
Answer: <img width="631" height="548" alt="image" src="https://github.com/user-attachments/assets/16cae978-681f-4a6e-9e50-c515a87ab8ef" />

- Do customers with higher salaries tend to have higher purchase amounts?
```python
eda_viz.groupby("Salary")["Purchase_Amount"].mean().plot(
    kind="line",
    marker="o",
    title="Average Purchase Amount by Salary",
    ylabel="Average Purchase"
)
plt.show()

fig, ax = plt.subplots()

ax.scatter(
    eda_viz["Age"],
    eda_viz["Salary"]
)

ax.set_title("Age vs Salary")
ax.set_xlabel("Age")
ax.set_ylabel("Salary")

plt.show()
```
Answer: <img width="626" height="553" alt="image" src="https://github.com/user-attachments/assets/a2b7ad35-4c95-4b61-8a74-1566a9efda6c" />

- Highest City Average vs Overall Average
```python
city_avg = (
    eda_viz.groupby("City")["Purchase_Amount"]
    .mean()
    .round(2)
)

highest_city = city_avg.idxmax()
highest_avg = city_avg.max()

overall_avg = round(
    eda_viz["Purchase_Amount"].mean(),
    2
)

difference = round(
    highest_avg - overall_avg,
    2
)

print("City:", highest_city)
print("City average:", highest_avg)
print("Overall average:", overall_avg)
print("Difference:", difference)

comparison = {
    highest_city: highest_avg,
    "Overall Average": overall_avg
}

plt.bar(
    comparison.keys(),
    comparison.values()
)

plt.title("Highest City Average vs Overall Average")
plt.ylabel("Average Purchase Amount")

plt.show()
```
Answer: <img width="641" height="552" alt="image" src="https://github.com/user-attachments/assets/3347f8ce-7192-42e3-8017-a8316ba00582" />



