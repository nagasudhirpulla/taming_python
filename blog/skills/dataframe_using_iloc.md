## Skill - Selecting a subset of DataFrame based on index / column positions using 'iloc' function
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
* Suppose for a dataframe `df` if you want to get a subset DataFrame with 2nd to 5th columns and 12th to 28th rows, we can use `df.iloc[11:28, 1:5]`

* If we want all rows but only 5th to 9th columns then we can use `df.iloc[:, 4:9]`

* If we want all columns but only 45th to 64th rows then we can use `df.iloc[44:64, :]`

* If we want all rows but only 1,5,8 columns then we can use `df.iloc[:, [1,5,8]]` 

### Example
```python
import pandas as pd

# create DataFrame from csv
df = pd.read_csv('gen_schedules.csv')

# get 2nd to 5th columns and 12th to 28th rows
df1 = df.iloc[11:28, 1:5]
print(df1)

# get all rows but only 5th to 9th columns
df2 = df.iloc[:, 4:9]
print(df2)

# get all columns but only 45th to 64th rows
df3 = df.iloc[44:64, :]
print(df3)

# get all rows but only 1,5,8 column indexes
df4 = df.iloc[:, [1,5,8]]
print(df4)
```

A similar function is [loc](https://nagasudhir.blogspot.com/2020/05/using-loc-function-of-dataframe.html), but it uses indexes and column names to get a subset of DataFrame.

### Video
Video for this post can be found [here](https://youtu.be/hxF6pdQc5ZU)

<iframe width="560" height="315" src="https://www.youtube.com/embed/hxF6pdQc5ZU" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* Official tutorial - https://pandas.pydata.org/pandas-docs/stable/getting_started/intro_tutorials/03_subset_data.html#min-tut-03-subset

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFVzaW5nIGlsb2MgZnVuY3
Rpb24gb2YgRGF0YUZyYW1lXG5hdXRob3I6IE5hZ2FzdWRoaXIg
UHVsbGFcbmRhdGU6ICcyMDIwLTA1LTA2J1xudGFnczogJ2xlYX
JuaW5nLCBweXRob24sIHRhbWluZ19weXRob25fc2tpbGwnXG5j
YXRlZ29yaWVzOiB0YW1pbmdfcHl0aG9uX3NraWxsXG4iLCJoaX
N0b3J5IjpbMzg1NTM3NzIyLDEzOTEwMDQwMzIsOTcwNjAxNTQz
LDY4NDQ4NDU2MiwxNzg0OTkyODgwLDE0NjEyOTY0OTddfQ==
-->