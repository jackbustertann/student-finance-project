## Student finance project

Calculating salary earned for each year, assuming a fixed inflation rate

```python
salary(initial_salary, inflation, years)
def salary(initial_salary, inflation, years):
    salary = []
    for year in range(years):
        salary.append((initial_salary)* (1 + (inflation/100))**year)
    return(salary)
 ```
 
Calculating the individual amount paid towards loan for each year

```python
def amount_paid_individual(initial_salary, inflation, years, percent_paid):
    amount = []
    for year in salary(initial_salary, inflation, years):
        amount.append(year * (percent_paid / 100))
    return(amount)
 ```
 
Calculating the remaining loan for each year, assuming a fixed interest rate

```python
def remaining_loan(initial_salary, inflation, years, percent_paid, initial_loan, interest):
    amount_left = []
    current_left = initial_loan
    for year in amount_paid_year(initial_salary, inflation, years, percent_paid):
        current_left = (current_left - year) * (1 + (interest/100))
        if current_left > 0:
            amount_left.append(current_left)
        else:
            amount_left.append(0)
    return(amount_left)
```

Calculating the total amount paid towards loan for each year

```python
def amount_paid_total(initial_salary, inflation, years, percent_paid, initial_loan, interest):
    total_amount = []
    current_amount = 0
    i = -1
    j = 0
    for year in amount_paid_year(initial_salary, inflation, years, percent_paid):
        current_amount += year
        total_amount.append(current_amount)
        i += 1
        if remaining_loan(initial_salary, inflation, years, percent_paid, initial_loan, interest)[i] <= 0:
            total_amount[i] = total_amount[i - j]
            j += 1
    return(total_amount)
```

Creating a dictionary containing all the values calculated for each year

```python
def dictionary(initial_salary, inflation, years, percent_paid, initial_loan, interest):
    years_list = [{'year': 0, 'salary': 0, 'amount paid': 0, 'total paid': 0, 'remaining loan': initial_loan}]
    salaries = salary(initial_salary, inflation, years)
    amounts_paid_individual = amount_paid_individual(initial_salary, inflation, years, percent_paid)
    amounts_paid_total = amount_paid_total(initial_salary, inflation, years, percent_paid, initial_loan, interest)
    remaining_loans = remaining_loan(initial_salary, inflation, years, percent_paid, initial_loan, interest)
    for i in range(years):
        years_list.append({'year': i + 1, 'salary': int(salaries[i]), 'amount paid': int(amounts_paid_individual[i]), 'total paid': int(amounts_paid_total[i]), 'remaining loan': int(remaining_loans[i])})    
    return(years_list)
```

Plot to show how changing the inflation rate effects the total amount paid to student finance after 30 years

```python
import plotly as plt
import plotly.graph_objs as go
plt.offline.init_notebook_mode(connected = True)

years = list(range(1,31))

zero_interest = go.Line({'x': years, 'y': amount_paid_total(25000, 0, 30, 9, 38000, 6), 'mode': 'lines', 'name': 'no pay rise'})
one_interest = go.Line({'x': years, 'y': amount_paid_total(25000, 1, 30, 9, 38000, 6), 'mode': 'lines', 'name': '1% pay rise'})
two_interest = go.Line({'x': years, 'y': amount_paid_total(25000, 2, 30, 9, 38000, 6), 'mode': 'lines', 'name': '2% pay rise'})
three_interest = go.Line({'x': years, 'y': amount_paid_total(25000, 3, 30, 9, 38000, 6), 'mode': 'lines', 'name': '3% pay rise'})
layout = go.Layout({'title': 'Total amount paid to student finance for different inflation rates, assuming a starting salary of 25k', 'xaxis': {'title':'year'}, 'yaxis': {'title':'total amount paid'}})                           
figure=go.Figure(data=[zero_interest, one_interest, two_interest, three_interest],layout=layout)
plt.offline.iplot(figure)
```
Plot to show how changing the starting salary effects the total amount paid to student finance after 30 years

```python
import plotly as plt
import plotly.graph_objs as go
plt.offline.init_notebook_mode(connected = True)

years = list(range(1,31))

twenty_five_start = go.Line({'x': years, 'y': amount_paid_total(25000, 2, 30, 9, 38000, 6), 'mode': 'lines', 'name': '25k'})
thirty_start = go.Line({'x': years, 'y': amount_paid_total(30000, 2, 30, 9, 38000, 6), 'mode': 'lines', 'name': '30k'})
thirty_five_start = go.Line({'x': years, 'y': amount_paid_total(35000, 2, 30, 9, 38000, 6), 'mode': 'lines', 'name': '35k'})
fourty_start = go.Line({'x': years, 'y': amount_paid_total(40000, 2, 30, 9, 38000, 6), 'mode': 'lines', 'name': '40k'})
layout_2 = go.Layout({'title': 'Total amount paid to student finance for different starting salaries, assuming a fixed inflation rate of 2%', 'xaxis': {'title':'year'}, 'yaxis': {'title':'total amount paid'}})                           
figure_2=go.Figure(data=[twenty_five_start, thirty_start, thirty_five_start, fourty_start],layout=layout_2)
plt.offline.iplot(figure_2)
```

