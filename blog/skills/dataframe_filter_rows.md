## Skill - Filter DataFrame rows
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

In this post, we will learn how to select only desired columns of a dataframe

<hr/>

#### Instructions to run the codes below
* Create a folder and place the csv file used in this post from [here](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/gen_schedules.csv)
* Open the folder in Visual Studio Code
* Create and work on python files in this folder

The excel files should look like the image below 
![excel_file_illustration](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/all_gen_data.png)

Suppose in a DataFrame `df` we want to get rows with values in column 'A' greater than 20, then we use `df[df['A']>20]`

### Example
```python
import pandas as pd
# create dataframe from excel
df = pd.read_csv('gen_schedules.csv')

print('Number of rows in df = {0}'.format(df.shape[0]))
# this prints Number of rows in df = 100

# filter the rows with CGPL values greater than 2200
filteredDf = df[df['CGPL']>2200]

print('Number of rows in filteredDf = {0}'.format(filteredDf.shape[0]))
# this prints Number of rows in filteredDf = 65

# filter the rows with CGPL values greater than 2200 and KSTPS7 less than 450
# 
filteredDf2 = df[(df['CGPL']>2200) & (df['KSTPS7']<450)]

print('Number of rows in filteredDf2 = {0}'.format(filteredDf2.shape[0]))
# this prints Number of rows in filteredDf2 = 10
```

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* Official tutorial - https://pandas.pydata.org/pandas-docs/stable/getting_started/intro_tutorials/03_subset_data.html#min-tut-03-subset

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk0NzUxNjg5NSw2MzgzNzc3OTcsLTE3Nj
UwNzUxMjIsLTEwMjI5NTUxMjFdfQ==
-->