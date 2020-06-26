## Skill - Add or subtract months to date in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Python datetime library](https://nagasudhir.blogspot.com/2020/05/datetime-library-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

`datetime` module in python is very useful in manipulating date-times.
`calendar` module in python is very useful in performing general calendar related functions
<hr/>
In this post we will learn how to add months to a datetime in python

Let number of months to add to a particular datetime be k

The algorithm we are using is as follows
* Add floor(input month - 1 + k) to input year component to get result year component
* Result month component would be (input month -1 + k)%12 + 1
* Result day component would be minimum of input date component and max date of that result month (For example we cant have day component as 30 in February month)
* hour, minute, seconds and microsecond components of result time will be the same as input datetime

If implementation of above algorithm as a function in python would be
```python
# import datetime and calendar modules
import datetime as dt
import calendar

def addMonths(inpDt, mnths):
  tmpMnth = inpDt.month - 1 + mnths

  # Add floor((input month - 1 + k)/12) to input year component to get result year component
  resYr = inpDt.year + tmpMnth // 12

  # Result month component would be (input month - 1 + k)%12 + 1
  resMnth = tmpMnth % 12 + 1

  # Result day component would be minimum of input date component and max date of the result month (For example we cant have day component as 30 in February month)
  # Maximum date in a month can be found using the calendar module monthrange function as shown below
  resDay = min(inpDt.day, calendar.monthrange(resYr,resMnth)[1])

  # construct result datetime with the components derived above
  resDt = dt.datetime(resYr, resMnth, resDay, inpDt.hour, inpDt.minute, inpDt.second, inpDt.microsecond)

  return resDt

# let's test our function with current time
nowDt = dt.datetime.now()

print('Now =', end=' ')
print(nowDt)

print('Now + 2 months =', end=' ')
print(addMonths(nowDt, 2))
```

In the above code, in order to get the maximum date for a given month (mnth) of a year (yr), we use the following function from calendar module
```python
calendar.monthrange(yr, mnth)[1]
```

You can use this function in your own projects directly from the algorithm implementation code written above

#### Points to remember
* If we 

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/ or https://repl.it/

### You can practice here


<hr/>

### References
* Official documentation - https://docs.python.org/3/library/calendar.html
* verified stackoverflow answer - https://stackoverflow.com/questions/4130922/how-to-increment-datetime-by-custom-months-in-python-without-using-library

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEFkZCBvciBzdWJ0cmFjdC
Btb250aHMgdG8gZGF0ZSBpbiBweXRob25cbmF1dGhvcjogTmFn
YXN1ZGhpciBQdWxsYVxuZGF0ZTogJzIwMjAtMDYtMjYnXG4iLC
JoaXN0b3J5IjpbNjk0MTA5MDk3LC0yNjk0OTA3MDMsMTMwNjc3
ODgyMSwtMjE0MzgyODcxNiwxMDY4MzQxMDAwLDczMDk5ODExNl
19
-->