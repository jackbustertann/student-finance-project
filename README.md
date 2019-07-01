## Student finance project

```python
def student_finance(initial_salary, pay_rise, percentage_of_salary, initial_loan, interest_rate, number_of_years):
    years = [{'year': 0, 'salary': 0, 'salary paid': 0, 'total paid': 0, 'loan remaining': initial_loan}]
    salary = initial_salary
    salary_paid = salary * (percentage_of_salary / 100)
    total_paid = salary_paid
    loan_remaining = (initial_loan - salary_paid) * (1 + (interest_rate / 100))
    for i in range(number_of_years):
        years.append({'year': i + 1, 'salary': int(salary), 'salary paid': int(salary_paid), 'total paid': int(total_paid), 'loan remaining': int(loan_remaining)})
        salary = salary * (1 + (pay_rise / 100))
        salary_paid = (salary * (percentage_of_salary / 100))
        loan_remaining = (loan_remaining - salary_paid) * (1 + (interest_rate / 100))
        if loan_remaining <= 0:
            salary_paid = 0
            loan_remaining = 0
            total_paid = total_paid
        else:
            total_paid = total_paid + (salary * (percentage_of_salary / 100))      
    return(years)
```
