## Skill - Advanced DataFrame rows filtering with lambda function
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

In this post, we will learn how to filter the rows of a DataFrame based on our desired criteria using lambda functions. This approach can accommodate complex filtering criteria since we will define the filtering criteria as a lambda function. The lambda function can access all the columns of each row while filtering the DataFrame rows

<hr/>

#### Instructions to run the codes below
* Create a folder and place the csv file used in this post from [here](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/gen_schedules.csv)
* Open the folder in Visual Studio Code
* Create and work on python files in this folder

The excel files should look like the image below 
![excel_file_illustration](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/all_gen_data.png)

### Example
```python
import pandas as pd
# create dataframe from excel
df = pd.read_csv('gen_schedules.csv')

print('Number of rows in df = {0}'.format(df.shape[0]))
# this prints Number of rows in df = 100

# filter the rows with VSTPS_III values greater than VSTPS_IV
filteredDf = df[df.apply(lambda x: x["VSTPS_III"]>x["VSTPS_IV"], axis=1)]

print('Number of rows in filteredDf = {0}'.format(filteredDf.shape[0]))
# this prints Number of rows in filteredDf = 34
```

### Video
Video for this post can be found [here](https://youtu.be/KVcJH6F25uE)

<iframe width="560" height="315" src="https://www.youtube.com/embed/KVcJH6F25uE" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### References
* stack overflow post - https://stackoverflow.com/questions/11418192/pandas-complex-filter-on-rows-of-dataframe
* DataFrame apply function documentation - https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.apply.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoiZXh0ZW5zaW9uczpcbiAgcHJlc2V0Oi
AnJ1xuZGF0ZTogJzIwMjAtMDItMjAnXG50aXRsZTogQWR2YW5j
ZWQgRGF0YUZyYW1lIHJvd3MgZmlsdGVyaW5nIHdpdGggbGFtYm
RhIGZ1bmN0aW9uc1xuYXV0aG9yOiBOYWdhc3VkaGlyIFB1bGxh
XG50YWdzOiAndGFtaW5nX3B5dGhvbl9za2lsbCwgdGFtaW5nX3
B5dGhvbidcbiIsImhpc3RvcnkiOlstMTExMDQyNDI1NiwtNjY0
NjU4NjA1LDEzMTQ3NjQ5NDcsLTE5OTg4MDg1ODIsLTE0MzY3NT
YxMDYsLTE2NTk2MTU1OTEsMzcxMjIwM119
-->