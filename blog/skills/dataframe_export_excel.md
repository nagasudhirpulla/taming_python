## Skill - Export DataFrame to excel or csv
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

Suppose in a DataFrame `df` 

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

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/RevolvingAngryFrontend?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### References
* `to_excel` function - https://pandas.pydata.org/pandas-docs/version/0.15.0/generated/pandas.DataFrame.to_excel.html
* `to_csv` funct

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU0MTgyMDcwNF19
-->