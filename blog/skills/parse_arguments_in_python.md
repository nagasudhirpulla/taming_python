## Skill - parse command line arguments in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will understand how to read command line arguments using `argparse` module

Install **argparse** module by entering the following in command prompt
```
pip install argparse
```

#### Example
```python
import pandas as pd

dfCsv = pd.read_csv('gen_schedules.csv')
print(dfCsv)

dfExcel = pd.read_excel('gen_schedules.xlsx')
print(dfExcel)
```

### read data from a specific excel sheet using "sheet_name" option
`sheet_name` can be the name of the sheet or the position of the sheet (zero-based)
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

# read only columns with positions(zero-based) 2,6,8
dfCsv = pd.read_csv('gen_schedules.csv', usecols=[2,6,8])
print(dfExcel)

# read only columns A,C,E:H
dfExcel = pd.read_excel('gen_schedules.xlsx', usecols=['A,C,E:H'])
print(dfExcel)
```
#### skip rows at the top during import using "skiprows" option
If the main excel/csv data starts after some rows, this option will be useful
```python
import pandas as pd

# skip first 5 rows and then read the excel data
dfExcel = pd.read_excel('gen_schedules.xlsx', skiprows=5)

print(dfExcel)
```

#### skip rows at the bottom during import using "skipfooter" option
If the main excel/csv data has unnecessary data at the end of the file, this option will be useful
```python
import pandas as pd

# skip the bottom 2 rows and then read the excel data
dfExcel = pd.read_excel('gen_schedules.xlsx', skipfooter=2)

print(dfExcel)
```

#### import only specific number of rows using "nrows" option
```python
import pandas as pd

# read only 50 rows
dfExcel = pd.read_excel('gen_schedules.xlsx', nrows=50)
print(dfExcel)
```

### export DataFrame to excel / csv using "to_excel " and "to_csv"
for more options to export data, read the official docs of [to_excel ](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_excel.html#pandas.DataFrame.to_excel) and [to_csv](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_csv.html)
```python
import pandas as pd

x = [
        {"Name": "Harris", "Age": 22, "Sex": "male"},
        {"Name": "Mr. William Henry", "Age": 35, "Sex": "male"},
        {"Name": "Miss. Elizabeth", "Age": 58, "Sex": "female"},
    ]

# export DataFrame to a file named out.csv
x.to_csv('out.csv')

# export DataFrame to a file named output.xlsx
x.to_excel('output.csv')

# export DataFrame to  C:\Users\Nagasudhir\Documents\Python Projects\taming_python\data.xlsx
x.to_excel(r'C:\Users\Nagasudhir\Documents\Python Projects\taming_python\data.xlsx')
```

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### You can practice here

<iframe height="800px" width="100%" src="https://repl.it/repls/UnfitUnsteadyExpertise?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### References
* Official tutorial - https://docs.python.org/3/library/argparse.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MDg3NTQxOV19
-->