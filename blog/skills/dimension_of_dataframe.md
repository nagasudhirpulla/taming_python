
## Skill - Getting the shape/dimension of DataFrame
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Pandas DataFrame Basics](https://nagasudhir.blogspot.com/2020/05/pandas-dataframe-basics.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

Pandas is a python library.
**DataFrame** is a data structure provided by the pandas library.

Please go through [Pandas DataFrame Basics](https://nagasudhir.blogspot.com/2020/05/pandas-dataframe-basics.html) to learn the basics of pandas DataFrame.

In this post, we will learn how to get the shape of a pandas dataframe using **shape** attribute

The shape attribute returns the shape of DataFrame as  (nRows, nColumns)
```python
import pandas as pd
# create a dataframe
x = {
	"Name": ["Harris", "Miss. Elizabeth"],
	"Age": [22, 58],
	"Sex": ["male", "female"]
	}
df = pd.DataFrame(x)

print(df.shape)
# this will print (2,3)

print('Number of rows = {0}'.format(df.shape[0]))
print('Number of columns = {0}'.format(df.shape[1]))
'''
this will print
Number of rows = 2
Number of columns = 3
'''
```

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### You can p

### References
* Official tutorial - https://pandas.pydata.org/pandas-docs/stable/getting_started/index.html
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IERpbWVuc2lvbiBvZiBhIE
RhdGFGcmFtZVxuYXV0aG9yOiBOYWdhc3VkaGlyIFB1bGxhXG50
YWdzOiAnbGVhcm5pbmcsIHB5dGhvbiwgdGFtaW5nX3B5dGhvbl
9za2lsbCdcbmNhdGVnb3JpZXM6IHRhbWluZ19weXRob25fc2tp
bGxcbmRhdGU6ICcyMDIwLTA1LTA0J1xuIiwiaGlzdG9yeSI6Wy
0xMjI5ODgyMDYxLC0xMTYyNjM1MTVdfQ==
-->