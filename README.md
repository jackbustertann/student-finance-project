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

```
import plotly as plt
import plotly.graph_objs as go
plt.offline.init_notebook_mode(connected = True)

years = list(range(0,31))
total_paid_zero = list(map(lambda item: item['total paid'], student_finance(25000, 0, 9, 38000, 6, 30)))
total_paid_one = list(map(lambda item: item['total paid'], student_finance(25000, 1, 9, 38000, 6, 30)))
total_paid_two = list(map(lambda item: item['total paid'], student_finance(25000, 2, 9, 38000, 6, 30)))
total_paid_three = list(map(lambda item: item['total paid'], student_finance(25000, 3, 9, 38000, 6, 30)))

trace_zero = go.Line({'x': years, 'y': total_paid_zero, 'mode': 'lines', 'name': 'no pay rise'})
trace_one = go.Line({'x': years, 'y': total_paid_one, 'mode': 'lines', 'name': '1% pay rise'})
trace_two = go.Line({'x': years, 'y': total_paid_two, 'mode': 'lines', 'name': '2% pay rise'})
trace_three = go.Line({'x': years, 'y': total_paid_three, 'mode': 'lines', 'name': '3% pay rise'})
layout = go.Layout({'title': 'Total amount paid to student finance for different pay rise rates, assuming a starting salary of 25k', 'xaxis': {'title':'year'}, 'yaxis': {'title':'total amount paid'}})                           
figure=go.Figure(data=[trace_zero, trace_one, trace_two, trace_three],layout=layout)
plt.offline.iplot(figure)
```

```
import plotly as plt
import plotly.graph_objs as go
plt.offline.init_notebook_mode(connected = True)

years = list(range(0,31))
total_paid_twenty_five = list(map(lambda item: item['total paid'], student_finance(25000, 2, 9, 38000, 6, 30)))
total_paid_thirty = list(map(lambda item: item['total paid'], student_finance(30000, 2, 9, 38000, 6, 30)))
total_paid_thirty_five = list(map(lambda item: item['total paid'], student_finance(35000, 2, 9, 38000, 6, 30)))
total_paid_fourty = list(map(lambda item: item['total paid'], student_finance(40000, 2, 9, 38000, 6, 30)))

trace_twenty_five = go.Line({'x': years, 'y': total_paid_twenty_five, 'mode': 'lines', 'name': '25k'})
trace_thirty = go.Line({'x': years, 'y': total_paid_thirty, 'mode': 'lines', 'name': '30k'})
trace_thirty_five = go.Line({'x': years, 'y': total_paid_thirty_five, 'mode': 'lines', 'name': '35k'})
trace_fourty = go.Line({'x': years, 'y': total_paid_fourty, 'mode': 'lines', 'name': '40k'})
layout_2 = go.Layout({'title': 'Total amount paid to student finance for different starting salaries, assuming a fixed pay rise rate of 2%', 'xaxis': {'title':'year'}, 'yaxis': {'title':'total amount paid'}})                           
figure_2=go.Figure(data=[trace_twenty_five, trace_thirty, trace_thirty_five, trace_fourty],layout=layout_2)
plt.offline.iplot(figure_2)
```
