## Skill - Selecting a subset of DataFrame using 'loc' function
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

#### Instructions to run the codes below
* Create a folder and place the csv file used in this post from [here](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/gen_schedules.csv)
* Open the folder in Visual Studio Code
* Create and work on python files in this folder

The excel files should look like the image below 
![excel_file_illustration](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/all_gen_data.png)
The `loc` function of DataFrame can get a subset of DataFrame using the index values (for filtering rows) and column names (for filtering columns).



A similar function is [iloc](https://nagasudhir.blogspot.com/2020/05/using-iloc-function-of-dataframe.html), but it uses row and column positions to get a subset of DataFrame

### Example
```python
import pandas as pd

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
```

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* Official tutorial - https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.loc.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFVzaW5nIGxvYyBmdW5jdG
lvbiBvZiBEYXRhRnJhbWVcbmF1dGhvcjogTmFnYXN1ZGhpciBQ
dWxsYVxudGFnczogJ2xlYXJuaW5nLCBweXRob24sIHRhbWluZ1
9weXRob25fc2tpbGwnXG5jYXRlZ29yaWVzOiB0YW1pbmdfcHl0
aG9uX3NraWxsXG5kYXRlOiAnMjAyMC0wNS0wNydcbiIsImhpc3
RvcnkiOls2MDY1NjUzMjUsLTY3MTY0MDM3OSwtODgyNDEyNDAs
ODA1NDg0ODEzXX0=
-->