## Skill - Iterate over a time interval using pandas date_range

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Pandas DataFrame Basics](https://nagasudhir.blogspot.com/2020/05/pandas-dataframe-basics.html)
* [datetime module in Python](https://nagasudhir.blogspot.com/2020/05/datetime-library-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

pandas ```date_range``` function can be used to split a time range based on a variety of frequency options


### split time interval by a specified time period
```python
# import pandas module
import pandas as pd

startDt = dt.datetime(2020,1,1)
endDt = dt.datetime(2020,2,1)

splitDates = pd.date_range(startDt, endDt, freq=)

print('The series is')
print(s)

# convert series to dictionary using to_dict() function on series
sDict = s.to_dict()

print('The dictionary derived from series is ')
print(sDict)
# This should print
# {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5, 'f': 6}
```

### converting dictionary to a pandas series using pd.Series
```python
import pandas as pd

d = {"firstName":"John", "lastName": "Doe"}

s = pd.Series(d)

print(s)
# this will print
"""
firstName    John
lastName      Doe
dtype: object
"""
```

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* Official docs- https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.date_range.html
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMDA3NTg0MTBdfQ==
-->