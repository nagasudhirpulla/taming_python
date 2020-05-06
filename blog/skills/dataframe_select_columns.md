## Skill - Working with excel files and pandas DataFrames
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Pandas DataFrame Basics](https://nagasudhir.blogspot.com/2020/05/pandas-dataframe-basics.html)
* [Getting the column names of DataFrame](https://nagasudhir.blogspot.com/2020/05/getting-column-names-of-dataframe.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

Pandas is a python library.
**DataFrame** is a data structure provided by the pandas library.

Please go through [Pandas DataFrame Basics](https://nagasudhir.blogspot.com/2020/05/pandas-dataframe-basics.html) to learn the basics of pandas DataFrame.

In this post, we will learn how to select only desired columns of a dataframe

#### Instructions to run the codes below
* Create a folder and place the csv file used in this post from [here](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/gen_schedules.csv)
* Open the folder in Visual Studio Code
* Create and work on python files in this folder

The excel files should look like the image below 
![excel_file_illustration](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/all_gen_data.png)

Suppose a dataframe is `df` and if we want to get a single column data say column 'A', then we call df['A']. This will return a pandas *Series*.

Suppose a dataframe is `df` and if we want to get a data of multiple columns data say columns 'A', 'B', 'C', then we call df[['A', 'B', 'C']]. This will return a pandas *DataFrame*.

### Example Code
```python
import pandas as pd

# read the csv file into a dataframe named df
df = pd.read_csv('gen_schedules.csv')

# This dataframe contains many columns, but now we will select only KAPS, KHARGONE-I columns
filteredDf = df[["KAPS", "KHARGONE-I"]]
print(filteredDf)

print(type(filteredDf))
# this will print pandas.core.frame.DataFrame

# select only KHARGONE-I data
kharData = df["KHARGONE-I"]
print(kharData)

print(type(kharData))
# this will print pandas.core.series.Series
```


### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* Official tutorial - https://pandas.pydata.org/pandas-docs/stable/getting_started/intro_tutorials/03_subset_data.html#min-tut-03-subset

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMjk4MDM2OTgsOTkwNTU1MTIsLTY1Mz
IxMjc3OV19
-->