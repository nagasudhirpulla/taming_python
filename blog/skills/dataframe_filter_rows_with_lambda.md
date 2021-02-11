## Skill - Advanced DataFrame rows filtering with lambda functions
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Pandas DataFrame Basics](https://nagasudhir.blogspot.com/2020/05/pandas-dataframe-basics.html)
* [Filter DataFrame rows with conditional statements](https://nagasudhir.blogspot.com/2020/05/filter-dataframe-rows.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

Pandas is a python library.
**DataFrame** is a data structure provided by the pandas library.

Please go through [Pandas DataFrame Basics](https://nagasudhir.blogspot.com/2020/05/pandas-dataframe-basics.html) to learn the basics of pandas DataFrame.

In this post, we will learn how to filter the rows of a DataFrame based on our desired criteria using lambda functions. This approach can accommodate complex filtering criteria since we will define the filtering criteria as a lambda function. The lambda function can access all the columns of each row while filtering the rows

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
# we can achieve this via the logical operator '&'
filteredDf2 = df[(df['CGPL']>2200) & (df['KSTPS7']<450)]

print('Number of rows in filteredDf2 = {0}'.format(filteredDf2.shape[0]))
# this prints Number of rows in filteredDf2 = 10
```
### Filter DataFrame rows based on null / Nan values
```python
import pandas as pd
df = pd.read_csv("gen_schdules.csv")
# filter rows which have only null values in "Time Block" column
dfWithNa = df[df["Time Block"].isna()]
# filter rows which have only non null values in "Time Block" column
dfWithoutNa = df[~df["Time Block"].isna()]
print(dfWithoutNa)
```

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/RevolvingAngryFrontend?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### References
* Official tutorial - https://pandas.pydata.org/pandas-docs/stable/getting_started/intro_tutorials/03_subset_data.html#min-tut-03-subset

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbNDgxNTQ0NDE1XX0=
-->