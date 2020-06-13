## Skill - Export DataFrame as excel or csv
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

In this post, we will learn how to export a pandas DataFrame to an excel or csv file using `to_excel` and `to_csv` function

<hr/>

### export using 'to_csv' and 'to_excel' functions
```python
# import pandas module
import pandas as pd
# create dataframe
df = pd.DataFrame([['a', 'b'], ['c', 'd']],
                   index=['row 1', 'row 2'],
                   columns=['col 1', 'col 2'])

# export dataframe as 'out.csv' file using 'to_csv' function
df.to_csv(r'C:\Users\Nagasudhir\Desktop\out.csv')

# export dataframe as 'out.xlsx' file using 'to_excel' function
df.to_excel(r'C:\Users\Nagasudhir\Desktop\out.xlsx')
```

### ignore index column in export file using 'index = False'
```python
# import pandas module
import pandas as pd
# create dataframe
df = pd.DataFrame([['a', 'b'], ['c', 'd']],
                   index=['row 1', 'row 2'],
                   columns=['col 1', 'col 2'])

# export dataframe as 'out.csv' but ignore index column in exported file
df.to_csv('out.csv', index=False)

# export dataframe as 'out.xlsx' but ignore index column in exported file
df.to_excel('out.xlsx', index=False)
```

### ignore column names header in export file using 'header = False'
```python
# import pandas module
import pandas as pd
# create dataframe
df = pd.DataFrame([['a', 'b'], ['c', 'd']],
                   index=['row 1', 'row 2'],
                   columns=['col 1', 'col 2'])

# export dataframe as 'out.csv' but ignore column names row in exported file
df.to_csv('out.csv', header=False)

# export dataframe as 'out.xlsx' but ignore column names row in exported file
df.to_excel('out.xlsx', header=False)
```

### export only specific columns using 'columns' input
```python
# import pandas module
import pandas as pd
# create dataframe
df = pd.DataFrame([['a', 'b', 'c'], ['d', 'e', 'f']],
                   index=['row 1', 'row 2'],
                   columns=['col 1', 'col 2', 'col3'])

# export dataframe as 'out.csv' but only export 'col1', 'col2' columns
df.to_csv('out.csv', header=False)

# export dataframe as 'out.xlsx' but only export 'col1', 'col2' columns
df.to_excel('out.xlsx', header=False)
```

### export to excel with a sheet name with 'sheet_name' input
```python
# import pandas module
import pandas as pd
# create dataframe
df = pd.DataFrame([['a', 'b'], ['c', 'd']],
                   index=['row 1', 'row 2'],
                   columns=['col 1', 'col 2'])

# export dataframe as 'out.xlsx' but with sheet name as 'hello' 
df.to_excel('out.xlsx', sheet_name='hello')
```

### export multiple DataFrames to a new excel file
```python
# import pandas module
import pandas as pd
# create dataframe
df = pd.DataFrame([['a', 'b'], ['c', 'd']],
                   index=['row 1', 'row 2'],
                   columns=['col 1', 'col 2'])

# export dataframe as 'out.xlsx' but with sheet name as 'hello' 
df.to_excel('out.xlsx', sheet_name='hello')
```

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### You can practice here


### References
* `to_excel` function - https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_excel.html#pandas.DataFrame.to_excel
* `to_csv` function - https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_csv.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEV4cG9ydCBEYXRhRnJhbW
UgYXMgZXhjZWwgb3IgY3N2XG5hdXRob3I6IE5hZ2FzdWRoaXIg
UHVsbGFcbmRhdGU6ICcyMDIwLTA2LTEzJ1xudGFnczogJ2xlYX
JuaW5nLCBweXRob24sIHRhbWluZ19weXRob25fc2tpbGwnXG5j
YXRlZ29yaWVzOiB0YW1pbmdfcHl0aG9uX3NraWxsXG4iLCJoaX
N0b3J5IjpbLTY2NzExODEzNywtMTMyMzc2NTMyNF19
-->