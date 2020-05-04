## Skill - Working with Excel and pandas DataFrames
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Pandas DataFrame Basics](https://nagasudhir.blogspot.com/2020/05/pandas-dataframe-basics.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

Pandas is a python library.
**DataFrame** is a data structure provided by the pandas library.
Please go through [Pandas DataFrame Basics](https://nagasudhir.blogspot.com/2020/05/pandas-dataframe-basics.html) to learn the basics of pandas DataFrame.

In this post, we will learn common excel input output scenarios with pandas DataFrames

#### Instructions to run the codes below
* Create a folder and place the csv file used in this post from [here](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/gen_schedules.csv) and excel file used in this post from [here](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/gen_schedules.xlsx)
* Open the folder in Visual Studio Code
* Create and work on python files in this folder

#### Creating a DataFrame from excel files using 'read_csv' or 'read_excel'
read the documentation of `read_csv` [here](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html)
read the documentation of `read_excel` [here](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_excel.html)
```python
import pandas as pd

dfCsv = pd.read_csv('gen_schedules.csv')
print(dfCsv)

dfExcel = pd.read_excel('gen_schedules.xlsx')
print(dfExcel)
```

#### read data from a specific excel sheet using "sheet_name" option
**sheet_name** can be the name of the sheet or the position of the sheet (zero-based)
```python
import pandas as pd

dfExcel = pd.read_excel('gen_schedules.xlsx', sheet_name='Sheet1')
print(dfExcel)
```

#### import excel/csv data without header using "header" option
```python
import pandas as pd

dfExcel = pd.read_excel('gen_schedules.xlsx', header=None)
print(dfExcel)

dfCsv = pd.read_csv('gen_schedules.csv', header=None)
print(dfExcel)
```

#### import only specific columns with "usecols" option
```python
import pandas as pd

# read only three columns with headers CGPL,GADARWARA-I,GANDHAR-APM
dfExcel = pd.read_excel('gen_schedules.xlsx', usecols=['CGPL','GADARWARA-I','GANDHAR-APM'])
print(dfExcel)

dfCsv = pd.read_csv('gen_schedules.csv', header=None)
print(dfExcel)
```

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* Official tutorial - https://pandas.pydata.org/pandas-docs/stable/getting_started/index.html
*  
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFdvcmtpbmcgd2l0aCBFeG
NlbCBhbmQgcGFuZGFzIERhdGFGcmFtZXNcbmF1dGhvcjogTmFn
YXN1ZGhpciBQdWxsYVxudGFnczogJ2xlYXJuaW5nLCBweXRob2
4sIHRhbWluZ19weXRob25fc2tpbGwnXG5jYXRlZ29yaWVzOiB0
YW1pbmdfcHl0aG9uX3NraWxsXG5kYXRlOiAnMjAyMC0wNS0wNC
dcbiIsImhpc3RvcnkiOlstMTAyMDMxMjMyNCwtODg3ODI5Mzk1
LDE3NTk0NTE1ODEsNjEyOTM3MTI5LDEyNjI4NDU1MDZdfQ==
-->