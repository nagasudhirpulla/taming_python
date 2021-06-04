
## Skill - Reshaping Pandas Dataframe using pivot and melt functions
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

In this post, we will learn how to reshape a pandas DataFrame using `pivot`, `pivot_table` and `melt` functions
<hr/>

Dataframe `pivot` function is similar to the pivot in Excel Tables

#### Excel files used in this post
* Excel files used in this post can be found at
	* [pivot_data_1.xlsx](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/pivot_data_1.xlsx)
	* [melt_data_1.xlsx](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/melt_data_1.xlsx)

pivot and 

![pivot_melt_illustration](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/pivot_melt_illustration.png)
As shown in the above image, using pivot, we can add convert column(s) data into 
### pivot example
```python
import  pandas  as  pd
import  datetime  as  dt

df = pd.read_excel('pivot_data_1.xlsx')
print(df)

df1 = df.pivot(index="id", columns="attribute", values="value")
print(df1)
```

### melt example
```python
import  pandas  as  pd
import  datetime  as  dt

df = pd.read_excel('melt_data_1.xlsx')
print(df)

df1 = df.melt(id_vars=["id"])
print(df1)
```


<hr/>
### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* pivot - https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.pivot.html
* pivot_table  - https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.pivot_table.html
* melt - https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.melt.html#pandas.DataFrame.melt

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExODA5NjM0MywxMjExMTM4ODUwLDE4Mj
kzMTk4MDEsNjQ4NjI3MTgyLDEyMTQyMTM3MSw4NTgwNTg3NDMs
MTAwOTEzNzY1OSwtMTEyNjI4NjE4MSwtMTM1NjA1Mjc2Ml19
-->