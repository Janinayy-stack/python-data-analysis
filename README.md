# 🧮 Salary Calculator

## 📌 Solution

## Create a simple calculator that calculates annual salary based on a person's monthly salary.

```python
monthly_salary = float(input("Enter your monthly salary: "))
total_mo = float(input("Enter your monthly expenses: "))
tax_rate = 0.12
savings_rate = 0.10

salary_tax = monthly_salary * tax_rate
monthly_tax = monthly_salary - salary_tax
savings = round(monthly_tax * savings_rate)

remaining = monthly_tax - total_mo - savings

print("Tax:", round(salary_tax))
print("Salary after tax:", round(monthly_tax))
print("Savings:", savings)
print("Money available:", round(remaining))
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
def calculate_tax(monthly_salary):
    tax_salary = monthly_salary * tax_rate
    return tax_salary

tax = calculate_tax(135000)
print(tax)
```
## Get the salary after tax, savings, and remaining money
```python
def salary_after_tax(monthly_salary, tax):
    salary1 = monthly_salary - tax
    return salary1

salarytax = salary_after_tax(monthly_salary,tax)
print(salarytax)

def calculate_savings(salary_after, savings_rate):
    final_savings = salary_after * savings_rate
    return final_savings

finalsavings = calculate_savings(salarytax, savings_rate)
print(finalsavings)

def calculate_remaining(salary_after, expenses, savings):
    remained = salary_after - expenses - savings
    return remained

finalremaining = calculate_remaining(salarytax, total_mo, finalsavings)
print(finalremaining)
```
## Combination of conditionals and functions
```python
def get_budget_status(remaining):
    if remaining >= 10000:
        status = "Healthy Budget"
    elif remaining >= 5000:
        status = "Tight Budget"
    else:
        status = "Needs Review"
    return status

finalstatus = get_budget_status(finalremaining)
print(finalstatus)
```

Whole process: <img width="301" height="267" alt="image" src="https://github.com/user-attachments/assets/e8e44138-da64-49da-814f-bd2c7ec44689" />
