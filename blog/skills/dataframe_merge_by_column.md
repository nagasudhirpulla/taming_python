## Skill - Join two DataFrames on a column
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Pandas DataFrame Basics](https://nagasudhir.blogspot.com/2020/05/pandas-dataframe-basics.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

Pandas is a python library.
**DataFrame** is a data structure provided by the pandas library.

Please go through [Pandas DataFrame Basics](https://nagasudhir.blogspot.com/2020/05/pandas-dataframe-basics.html) to learn the basics of pandas DataFrame.

In this post, we will learn how to join two DataFrames using `merge` function

In order to merge a DataFrame with another either it's index or column can be used

<hr/>

### Merge on index column
```python
# import pandas module
import pandas as pd

# create a dataframe
df1 = pd.DataFrame({'cleft': ['foo', 'bar', 'baz', 'foo'],'value': [1, 2, 3, 5]})
print(df1)
"""
prints
cleft  value
0   foo      1
1   bar      2
2   baz      3
3   foo      5
"""

# create another dataframe
df2 = pd.DataFrame({'cright': ['foo', 'bar', 'baz', 'foo'],'value': [5, 6, 7, 8]})
print(df2)
"""
prints
  cright  value
0    foo      5
1    bar      6
2    baz      7
3    foo      8
"""

# merge dataframes on index
df3 = df1.merge(df2, left_index=True, right_index=True)
print(df3)
"""
this prints
cleft  value_x cright  value_y
0   foo        1    foo        5
1   bar        2    bar        6
2   baz        3    baz        7
3   foo        5    foo        8
"""

# merge dataframes on index and use custom suffix for overlapping columns
df3 = df1.merge(df2, left_index=True, right_index=True, suffixes=('_lft', '_rgt'))
print(df3)
"""
this prints
cleft  value_lft cright  value_rgt
0   foo          1    foo          5
1   bar          2    bar          6
2   baz          3    baz          7
3   foo          5    foo          8
"""
```
We can see that `merge` function adds suffixes (which are also configurable) to overlapping columns in the output DataFrame

### Merge on column names
```python
# import pandas module
import pandas as pd

# create a dataframe
df1 = pd.DataFrame({'cleft': ['foo', 'bar', 'baz', 'foo'],'value': [1, 2, 3, 5]})

# create another dataframe
df2 = pd.DataFrame({'cright': ['foo', 'bar', 'baz', 'foo'],'value': [5, 6, 7, 8]})

# merge dataframes on column names
df3 = df1.merge(df2, left_index=True, right_index=True)
print(df3)
```
<hr/>

Please read this [official documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.merge.html) for getting know about more options and examples

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### You can practice here


### References
* Official docs - https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.merge.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYwMDk5MDIzNiwyMDkzNzIwNzEyLC00Nz
g2MDgzNTMsLTU4MDYxMzE0MSwtNzcwMDg3NDc3LC0xNjQ0MjU4
MDE5LC0xMTg2MTUwOTc4XX0=
-->