python notes -  http://thomas-cokelaer.info/tutorials/python/basics.html#the-basics

matplotlib overview tutorial - https://towardsdatascience.com/data-visualization-using-matplotlib-16f1aae5ce70


### TODOS
* dataframe rename columns using dict and lists
```python
#%%
# import pandas module
import pandas as pd

# read the data
df = pd.read_csv('ramen-ratings.csv')

# %%
# get the column names as a list
colNames = df.columns.tolist()
print(colNames)

#%%
# rename targeted column names via the rename method 
df.rename(columns={"Review #": "review"}, inplace=True)
print(df.columns)

# %%
# change all the columns by assigning a new list of columns
newCols = [x.strip().replace(" ", "_").lower() for x in df.columns]
df.columns = newCols

newCols = ["revw", "brnd", "varty", "stl", "cntry", "strs", "tptn"]
df.columns = newCols
```
* convert dataframe into list of dictionaries using df.to_dict('records')
* process dataframes and dbf in chunks
* docxtpl tutorial for templates, plots, images etc
* Histogram in python
* Manage application configuration or application secrets in Excel  
* global variables and using them inside functions- https://instructobit.com/tutorial/108/How-to-share-global-variables-between-files-in-Python
* python subprocess communication - https://eli.thegreenplace.net/2017/interacting-with-a-long-running-child-process-in-python/
* rounding of decimals while printing and rounding the number itself
* flask server basics
* naming conventions for classes (nouns), variables (nouns), functions (verbs), using camel case, avoid obvious names and use contextual names for better readability



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MzIzOTIwODcsLTIyOTYyOTU1NywxOT
I0MjYzOTg4LDEzOTEzOTQwNjAsMTI1ODI4NjIzNywtODkwMjM5
MTAwLC0xMTQ0OTExNDM3LC0zNjQ1ODgxMzYsLTE2MDc1NTY0Nj
gsLTExOTM5ODk4NzAsOTkwNTEzMTExLC04ODExMzgzODEsLTk4
OTQ3NzI2MSwtMjA1NjQwNTU1MCwtOTc4NjczNDEsLTMyMzk4OD
E0OSwtMTkyMzc2Mzk0NywzOTQ1Mzc4NjksLTEzOTE0OTU2MDUs
LTIyMTg4OTk3NV19
-->