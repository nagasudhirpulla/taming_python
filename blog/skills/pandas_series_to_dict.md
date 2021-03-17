## Skill - Convert pandas Series to dictionary in python

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


### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/WorthwhileGoldenrodFolders?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

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
luZ19weXRob25fc2tpbGxcbiIsImhpc3RvcnkiOls2ODY0NTMy
NDcsMTExMzk1MzI4NCwxMTY2NDA3NTE5LDEyMDc5NDI4MDcsND
MyNzkyODc0LDEyMTkzNDY2ODksLTcwOTc4NDAzNiwtNjEzOTAx
OTM2LDE3ODA2NzIzODMsMTc4MDY3MjM4MywxNzgwNjcyMzgzXX
0=
-->