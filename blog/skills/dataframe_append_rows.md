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
this prints
   A  B
0  1  2
1  3  4
"""
# create another dataframe
df2 = pd.DataFrame([[5,6],[7,8]], columns=['A', 'B'])
print(df2)
"""
this prints
    A  B
0  5  6
1  7  8
"""

# append df2 to df1 using 'append' function
df3 = df1.append(df2)
print(df3)
"""
this prints
   A  B
0  1  2
1  3  4
0  5  6
1  7  8
"""

# append df2 to df1 and create a fresh index
df3 = df1.append(df2, ignore_index=True)
print(df3)
"""
this prints
   A  B
0  1  2
1  3  4
2  5  6
3  7  8
notice the index is reset due to ignore_index option
"""
```

### Using 'loc' to append a single row (if confident about the index)
Another way to append row to a DataFrame is to use [loc](https://nagasudhir.blogspot.com/2020/05/using-loc-function-of-dataframe.html) function. 
But use this method if are aware of the existing index of the DataFrame, otherwise we might loose the existing data
```python
# import pandas module
import pandas as pd

# create a DataFrame
df = pd.DataFrame([[1,2], [3,4]], columns=['A', 'B'])
print(df)
"""
this prints
   A  B
0  1  2
1  3  4
"""

# add a new row using loc
df.loc[2] = [5,6]
print(df)
"""
this prints
   A  B
0  1  2
1  3  4
2  5  6
"""

# instead of list we can append row using a pandas Series
df.loc[3] = pd.Series({"A":7, "B":9})

# we need not specify all column values while using pandas Series
# NaN will be used for unspecfied columns
df.loc[4] = pd.Series({"A":10})

print(df)
"""
this prints
   A  B
0  1  2
1  3  4
2  5  6
3  7  9
4  10  NaN
"""
```

### Video
Video for this post can be found [here](https://youtu.be/FX2RVHtA0WM)

<iframe width="560" height="315" src="https://www.youtube.com/embed/FX2RVHtA0WM" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

Please read this [official documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.append.html) for getting know about more options and examples

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

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
9uX3NraWxsXG4iLCJoaXN0b3J5IjpbOTc4MTk5OTc3LDE1MDM1
ODg0OTksNjUwODU2Mjc4LDE5MzkzMzM4NiwtMTM4NzI1ODE2OC
wtMTAyMjM2MTldfQ==
-->