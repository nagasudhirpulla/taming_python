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

In this post, we will learn how to select a subset of DataFrame using `iloc` function
<hr/>

The `loc` function of DataFrame can get a subset of DataFrame using the index values (for filtering rows) and column names (for filtering columns).

Suppose for a DataFrame df,
* ```df.loc[[<index_list>], [<columns_list>]]``` returns a subset DataFrame
* ```df.loc[[<True/False_list>], [<columns_list>]]``` returns a subset DataFrame
* ```df.loc['<index>', '<column_name>']``` returns a single value of the cell
* ```df.loc['<index>', [<columns_list>]]``` will return the row data as a *Series*.
* ```df.loc[[<index_list>], '<column_name>']``` will return the column data as a *Series*.

### Example: Getting values
```python
import pandas as pd

# create a dataframe with column names and row indexes
df = pd.DataFrame([[2, 3], [5, 6], [8, 9]],
     index=['cobra', 'viper', 'sidewinder'],
     columns=['max_speed', 'shield'])
print(df)
'''
            max_speed  shield
cobra               2       3
viper               5       6
sidewinder          8       9
'''

# get a single row with index 'viper'
print(df.loc['viper'])
# we can see that it returns the row as a series
'''
max_speed    5
shield       6
Name: viper, dtype: int64
'''

# get two rows with index 'viper' and 'sidewinder'
print(df.loc[['viper', 'sidewinder']])
# we can see that it returns the the subset DataFrame
'''
            max_speed  shield
viper               5       6
sidewinder          8       9
'''

# get cell value with row index 'cobra' and column name 'shield'
print(df.loc['cobra', 'shield'])
# this should print 3

# get rows starting from 'cobra' till 'viper' and column 'max_speed'
print(df.loc['cobra':'viper', 'max_speed'])
# since we asked for only one column we got a series
'''
cobra    2
viper    5
Name: max_speed, dtype: int64
'''

# get rows with values in 'shield' column greater than 6
print(df.loc[df['shield'] > 6])
'''
            max_speed  shield
sidewinder          8       9
'''

# get rows with values in 'shield' column greater than 6, but return only 'max_speed' column
print(df.loc[df['shield'] > 6, ['max_speed']])
'''
            max_speed
sidewinder          8
'''
```

### Example: Setting values
```python
import pandas as pd

# create a dataframe with column names and row indexes
df = pd.DataFrame([[2, 3], [5, 6], [8, 9]],
     index=['cobra', 'viper', 'sidewinder'],
     columns=['max_speed', 'shield'])
print(df)
'''
            max_speed  shield
cobra               2       3
viper               5       6
sidewinder          8       9
'''

# set a single value for rows with indexes 'viper', 'sidewinder' 
# and column 'shield'
df.loc[['viper', 'sidewinder'], ['shield']] = 30
print(df)
'''
            max_speed  shield
cobra               2       3
viper               5      30
sidewinder          8      30
'''

# set a single value of all columns of a row with index 'cobra'
df.loc['cobra'] = 10
print(df)
'''
            max_speed  shield
cobra              10      10
viper               5      30
sidewinder          8      30
'''

# set a single value of all the rows with column name 'max_speed'
df.loc[:, 'max_speed'] = 30
print(df)
'''
            max_speed  shield
cobra              30      10
viper              30      30
sidewinder         30      30
'''

# set a single for all columns of rows that satisfy a condition
df.loc[df['shield'] > 25] = 0
print(df)
'''
            max_speed  shield
cobra              30      10
viper               0       0
sidewinder          0       0
'''
```
<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### You can practice here


### References
* Official docs - https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.merge.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgzNTA5MTI5OSwtMTE4NjE1MDk3OF19
-->