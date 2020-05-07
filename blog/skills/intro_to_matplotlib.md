
## Skill - Pandas DataFrame Basics
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

Pandas is a python library.
**DataFrame** is a data structure provided by the pandas library
The image shown below tries to describe the anatomy of a DataFrame

![Pandas DataFrame anatomy](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/pandas_dataframe_anatomy.png)

![Pandas DataFrame illustration](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/pandas_dataframe_illustration.png)
* As shown above, a DataFrame is just like an excel sheet
* A DataFrame has columns, where each column has a name and position
* A DataFrame has rows, where each row also has a name and position
* The data in of a DataFrame lies in the cells of the DataFrame. Each cell has a specific row and column
* All the column labels of a DataFrame are called **columns**
* All the row labels of a DataFrame are called **index**

### Using Pandas DataFrame
* Open command prompt, type the command ```pip install pandas``` and press enter. This should install pandas library in your computer.
![pip install pandas in cmd](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/pip_install_pandas.png)
* In your python file write ```import pandas as pd``` at the top. Now you  can the variable `pd` to access pandas DataFrame

#### Creating a DataFrame with a dictionary of lists
```python
import pandas as pd
x = {
	"Name": ["Harris","Mr. William Henry","Miss. Elizabeth"],
	"Age": [22, 35, 58],
	"Sex": ["male", "male", "female"]
	}
df = pd.DataFrame(x)
 
print(df)
# this will print
'''
   Age               Name     Sex
0   22             Harris    male
1   35  Mr. William Henry    male
2   58    Miss. Elizabeth  female
'''
```
As shown above, each key of the dictionary will become a column in the DataFrame

#### Creating a DataFrame with a list of dictionaries
```python
import pandas as pd
x = [
        {"Name": "Harris", "Age": 22, "Sex": "male"},
        {"Name": "Mr. William Henry", "Age": 35, "Sex": "male"},
        {"Name": "Miss. Elizabeth", "Age": 58, "Sex": "female"},
    ]
df = pd.DataFrame(x)
 
print(df)
# this will print
'''
   Age               Name     Sex
0   22             Harris    male
1   35  Mr. William Henry    male
2   58    Miss. Elizabeth  female
'''
```

#### Creating a DataFrame with a list of lists
```python
import pandas as pd
x = [
        ["Harris", 22,"male"],
        ["Mr. William Henry", 35, "male"],
        ["Miss. Elizabeth", 58, "female"],
    ]
df = pd.DataFrame(x, columns=["Name", "Age", "Sex"])
 
print(df)
# this will print
'''
                Name  Age     Sex
0             Harris   22    male
1  Mr. William Henry   35    male
2    Miss. Elizabeth   58  female
'''
```

#### Creating a DataFrame from csv using 'read_csv'
read the complete documentation of `read_csv` [here](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html)
The csv used for this example can be found [here](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/df_beginner.csv)
```python
import pandas as pd

df = pd.read_csv('df_beginner.csv')

print(df)
# this will print
'''
                Name  Age     Sex
0             Harris   22    male
1  Mr. William Henry   35    male
2    Miss. Elizabeth   58  female
'''
```
This code can be run in Visual Studio Code as shown below. Make sure csv in the same folder as python file.
![read_csv_demo_vs_code](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/read_csv_demo.png)
#### Creating a DataFrame from excel using 'read_excel'
read the complete documentation of `read_excel` [here](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_excel.html)
The excel file used for this example can be found [here](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/df_beginner.xlsx)
```python
import pandas as pd

df = pd.read_excel('df_beginner.xlsx')

print(df)
# this will print
'''
                Name  Age     Sex
0             Harris   22    male
1  Mr. William Henry   35    male
2    Miss. Elizabeth   58  female
'''
```
This code can be run in Visual Studio Code as shown below. Make sure the xlsx file in the same folder as python file.
![read_csv_demo_vs_code](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/read_excel_demo.png)
### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* Official tutorial - https://pandas.pydata.org/pandas-docs/stable/getting_started/index.html
* https://www.geeksforgeeks.org/python-pandas-dataframe/
* installing pandas YouTube video - https://www.youtube.com/watch?v=nZVolpD_Nl4
* Image credits - ```https://www.geeksforgeeks.org```, ```https://pandas.pydata.org```
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1Njg0NjQ1NTBdfQ==
-->