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

![merge dataframes](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/merge_dataframes_cartoon_lakshmi.jpg)

In this post, we will learn how to join two DataFrames using `merge` function

In order to merge a DataFrame with another either it's index or column can be used

<hr/>

### Merge on index
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

Please read this [official documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.merge.html) for getting know about more options and examples

<hr/>

### Video
Video for this post can be found [here](https://youtu.be/_5PZMnHdrbY)

<iframe width="560" height="315" src="https://www.youtube.com/embed/_5PZMnHdrbY" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* Official docs - https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.merge.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEpvaW4gdHdvIERhdGFGcm
FtZXMgb24gYSBjb2x1bW5cbmF1dGhvcjogTmFnYXN1ZGhpciBQ
dWxsYVxuZGF0ZTogJzIwMjAtMDYtMDUnXG50YWdzOiAnbGVhcm
5pbmcsIHB5dGhvbiwgdGFtaW5nX3B5dGhvbl9za2lsbCdcbmNh
dGVnb3JpZXM6IHRhbWluZ19weXRob25fc2tpbGxcbiIsImhpc3
RvcnkiOlstMjAwNzE2ODQ3MiwtMTUxMDMyMjc1OSwxNzg3NjI1
OTY5LDQ4MTk2NjAwNiwyMTM2NTQwMzc5LDE3NjY5Nzc5MDYsLT
EyMzg3MDMzNTYsMjA5MzcyMDcxMiwtNDc4NjA4MzUzLC01ODA2
MTMxNDEsLTc3MDA4NzQ3NywtMTY0NDI1ODAxOSwtMTE4NjE1MD
k3OF19
-->