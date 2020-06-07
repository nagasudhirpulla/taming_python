## Skill - Append rows or DataFrames to a pandas DataFrame
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


In this post, we will learn how to append rows or DataFrames to a pandas DataFrame using the `append` function


<hr/>

### Using the 'append' function
```python
# import pandas module
import pandas as pd

# create a dataframe
df1 = pd.DataFrame([[1,2],[3,4]], columns=['A', 'B'])
print(df1)
"""
prints
   
"""

# create another dataframe
df2 = pd.DataFrame([[5,6],[7,8]], columns=['A', 'B'])
print(df2)
"""
prints
    
"""

# append df2 to df1
df3 = df1.append(df2)
print(df3)
"""
this prints
   
"""

# append df2 to df1 and create a fresh index
df3 = df1.append(df2, ignore_index=True)
print(df3)
"""
this prints
   
"""
```
We can see that `merge` function adds suffixes (which are also configurable) to overlapping columns in the output DataFrame

### Merge on column names or a common column name
```python
# import pandas module
import pandas as pd

# create a dataframe
df1 = pd.DataFrame({'cleft': ['foo', 'bar', 'baz', 'foo'],'value': [1, 2, 3, 5]})

# create another dataframe
df2 = pd.DataFrame({'cright': ['foo', 'bar', 'baz', 'foo'],'value': [5, 6, 7, 8]})

# merge dataframes on column names
df3 = df1.merge(df2, left_on='cleft', right_on='cright')
print(df3)
"""
this prints
    cleft  value_x cright  value_y
0   foo        1    foo        5
1   foo        1    foo        8
2   foo        5    foo        5
3   foo        5    foo        8
4   bar        2    bar        6
5   baz        3    baz        7
"""

# merge on a column name common to both dataframes
df3 = df1.merge(df2, on='value')
print(df3)
"""
this prints
  cleft value cright
0 foo 5 foo
"""
```
In the above example, only one row is present, since only one row has came 'value' column in both DataFrames. 
This is called an **inner join** in which only rows with common values of the merging columns are present in the output DataFrame

### Type of join in merge function using 'how' input
* If `how = 'inner'`, then only rows with same values in the joining columns of both DataFrames are considered in output.
* If `how = 'outer'`, then all the rows will be considered in the output
* If `how = 'left'`, then all the rows of the left DataFrame will be considered in the output. If the values in right DataFrame will be `NaN` if corresponding column value is not present
* If `how = 'right'`, then all the rows of the right DataFrame will be considered in the output. If the values in left DataFrame will be `NaN` if corresponding column value is not present

```python
# import pandas
import pandas as pd

# create a dataframe
df1 = pd.DataFrame({'cleft': ['foo', 'bar', 'baz', 'foo'],'value': [1, 2, 3, 5]})

# create another dataframe
df2 = pd.DataFrame({'cright': ['foo', 'bar', 'baz', 'foo'],'value': [5, 6, 7, 8]})

# merge on a column name with join type as 'inner'
df3 = df1.merge(df2, on='value')
print(df3)
"""
this prints
  cleft value cright
0 foo 5 foo
"""

# merge on a column name with join type as 'outer'
df3 = df1.merge(df2, on='value', how='outer')
print(df3)
"""
this prints
  cleft  value cright
0   foo      1    NaN
1   bar      2    NaN
2   baz      3    NaN
3   foo      5    foo
4   NaN      6    bar
5   NaN      7    baz
6   NaN      8    foo
"""

# merge on a column name with join type as 'outer'
df3 = df1.merge(df2, on='value', how='left')
print(df3)
"""
this prints
  cleft  value cright
0   foo      1    NaN
1   bar      2    NaN
2   baz      3    NaN
3   foo      5    foo
"""

# merge on a column name with join type as 'outer'
df3 = df1.merge(df2, on='value', how='right')
print(df3)
"""
this prints
  cleft  value cright
0   foo      5    foo
1   NaN      6    bar
2   NaN      7    baz
3   NaN      8    foo
"""
```
<hr/>

Please read this [official documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.merge.html) for getting know about more options and examples

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/AngelicWrithingBotany?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### References
* Official docs - https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.append.html
* append rows - https://stackoverflow.com/questions/10715965/add-one-row-to-pandas-dataframe

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEFwcGVuZCByb3dzIG9yIE
RhdGFGcmFtZXMgdG8gYSBwYW5kYXMgRGF0YUZyYW1lXG5hdXRo
b3I6IE5hZ2FzdWRoaXIgUHVsbGFcbmRhdGU6ICcyMDIwLTA2LT
A3J1xudGFnczogJ2xlYXJuaW5nLCBweXRob24sIHRhbWluZ19w
eXRob25fc2tpbGwnXG5jYXRlZ29yaWVzOiB0YW1pbmdfcHl0aG
9uX3NraWxsXG4iLCJoaXN0b3J5IjpbODE4ODkzMjM0XX0=
-->