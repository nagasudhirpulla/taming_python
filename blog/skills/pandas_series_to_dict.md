## Skill - Convert pandas Series to dictionary and vice-versa in python

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Pandas DataFrame Basics](https://nagasudhir.blogspot.com/2020/05/pandas-dataframe-basics.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

Pandas is a python library.
**DataFrame** is a data structure provided by the pandas library

**Series** is like a column of a pandas dataframe. It has index, values and a series name
The image shown below tries to describe the anatomy of a DataFrame
<hr/>
In this post we are going to learn how to convert a pandas series into a dictionary using the `to_dict` function on the series. Dictionary is a set of key value pairs. An example can be seen below

```json
{
"firstname":"John",
"lastname": "Smith"
}
```

### converting pandas series to dictionary using to_dict function
```python
# import pandas module
import pandas as pd

# create a series for demonstration
s = pd.Series([1,2,3,4,5,6], index=['a', 'b', 'c', 'd', 'e', 'f'])

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

### Video
You can the video on this post [here](https://youtu.be/N_gx9mxl4lo)

<iframe width="560" height="315" src="https://www.youtube.com/embed/N_gx9mxl4lo" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* Official docs- https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.to_dict.html
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IENvbnZlcnQgcGFuZGFzIF
NlcmllcyB0byBkaWN0aW9uYXJ5IGluIHB5dGhvblxuYXV0aG9y
OiBOYWdhc3VkaGlyIFB1bGxhXG5kYXRlOiAnMjAyMC0wNy0wNC
dcbnRhZ3M6ICdweXRob24sIGxlYXJuaW5nLCB0dXRvcmlhbCwg
dGFtaW5nX3B5dGhvbl9za2lsbCdcbmNhdGVnb3JpZXM6IHRhbW
luZ19weXRob25fc2tpbGxcbiIsImhpc3RvcnkiOlstNjUwOTU5
MDQ0LDE2MDEwNjk3MTgsODg5OTAyNjY4LDExMTM5NTMyODQsMT
E2NjQwNzUxOSwxMjA3OTQyODA3LDQzMjc5Mjg3NCwxMjE5MzQ2
Njg5LC03MDk3ODQwMzYsLTYxMzkwMTkzNiwxNzgwNjcyMzgzLD
E3ODA2NzIzODMsMTc4MDY3MjM4M119
-->