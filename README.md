# 🧮 Salary Calculator

## 📌 Solution

## Create a simple calculator that calculates annual salary based on a person's monthly salary.

```python
monthly_salary = float(input("Enter your monthly salary: "))
total_mo = float(input("Enter your monthly expenses: "))
tax_rate = 0.12
savings_rate = 0.10

```
## CREATE Functions
```python
def calculate_tax(monthly_salary):
    tax_salary = monthly_salary * tax_rate
    return tax_salary

def salary_after_tax(monthly_salary, tax):
    salary1 = monthly_salary - tax
    return salary1

def calculate_savings(salary_after, savings_rate):
    final_savings = salary_after * savings_rate
    return final_savings

def calculate_remaining(salary_after, expenses, savings):
    remained = salary_after - expenses - savings
    return remained
```
## IF/ELIF/ELSE

```python
if remaining >= 10000:
    status = "Healthy Budget"
elif remaining >= 5000:
    status = "Tight Budget"
else:
    status = "Needs Review"

print("Budget status:", status)
```
## CREATE FUNCTIONS
```python
def get_budget_status(remaining):
    if remaining >= 10000:
        status = "Healthy Budget"
    elif remaining >= 5000:
        status = "Tight Budget"
    else:
        status = "Needs Review"
    return status
```
## CALCULATIONS
```python
tax = calculate_tax(monthly_salary)

salary_after = salary_after_tax(monthly_salary, tax)

finalsavings = calculate_savings(salary_after, savings_rate)

remaining = calculate_remaining(salary_after, total_mo, finalsavings)

finalstatus = get_budget_status(remaining)
```
## OUTPUT
```python
print("Monthly Salary:", monthly_salary)
print("Tax:", tax)
print("Salary After Tax:", salary_after)
print("Savings:", finalsavings)
print("Money Available:", remaining)
print("Budget Status:", finalstatus)
```

Whole process: <img width="292" height="179" alt="image" src="https://github.com/user-attachments/assets/52a6cb4a-5d32-40dd-942b-eaf59eac521c" />

