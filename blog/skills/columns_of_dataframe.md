## Skill - Getting the column names of DataFrame
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

In this post we will learn how to get the column names of a DataFrame using the **columns** attribute

```python
import pandas as pd
# create a dataframe
x = {
	"Name": ["Harris", "Miss. Elizabeth"],
	"Age": [22, 58],
	"Sex": ["male", "female"]
	}
df = pd.DataFrame(x)

# print the columns of DataFrame. This will return an index object
print(df.columns)
# Index([u'Age', u'Name', u'Sex'], dtype='object')

# print the list of columns of the DataFrame by passing it through 'list' function
print(list(df.columns))
# ['Age', 'Name', 'Sex']
```

### Video
Watch video on this post [here](https://youtu.be/XtcYVbJ-e7k)

<iframe width="560" height="315" src="https://www.youtube.com/embed/XtcYVbJ-e7k" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* Official tutorial - https://pandas.pydata.org/pandas-docs/stable/getting_started/index.html
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEdldHRpbmcgdGhlIGNvbH
VtbiBuYW1lcyBvZiBhIERhdGFGcmFtZVxuYXV0aG9yOiBOYWdh
c3VkaGlyIFB1bGxhXG5kYXRlOiAnMjAyMC0wNS0wNCdcbnRhZ3
M6ICdsZWFybmluZywgcHl0aG9uLCB0YW1pbmdfcHl0aG9uX3Nr
aWxsJ1xuY2F0ZWdvcmllczogdGFtaW5nX3B5dGhvbl9za2lsbF
xuIiwiaGlzdG9yeSI6Wy03Nzg1ODM2MSwtODM0NjYyMDI4XX0=

-->