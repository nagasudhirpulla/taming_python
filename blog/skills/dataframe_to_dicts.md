## Skill - Convert Pandas DataFrame to a list of dictionaries
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

In this post, we will learn how to convert pandas dataframe into a list of dictionaries

We might want to convert dataframe to list of objects for scenarios like sending the dataframe content via JSON API, creating rows for database table insertion etc.

The csv file used in this blog post can be downloaded [here](https://github.com/datasciencedojo/datasets/raw/master/titanic.csv)
 
<hr/>

### Dataframe to list of dictionaries using 'to_dict' method
```python
import pandas as pd

# read the csv file into a dataframe named df
df = pd.read_csv('titanic.csv')

# convert the dataframe into list of dictionaries using the .to_dict('records') methos
dfObjects = df.to_dict('records')
print(dfObjects)
```

### Create a dataframe from a list of dictionaries
```python
import pandas as pd

dfObjects = [{'PassengerId': 1, 'Survived': 0, 'Pclass': 3, 'Name': 'Braund, Mr. Owen Harris', 'Sex': 'male'},
{'PassengerId': 2, 'Survived': 1, 'Pclass': 1, 'Name': 'Cumings, Mrs. John Bradley (Florence Briggs Thayer)', 'Sex': 'female'}]

df = pd.DataFrame(data=dfObjects)
```

### Video
Video for this post can be found [here](https://youtu.be/V9Gn95OAYHs)

<iframe width="560" height="315" src="https://www.youtube.com/embed/V9Gn95OAYHs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### References
* Official Documentation - https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_dict.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NzQ5NTM3NTYsLTE3NTU2MzQ4NTcsMT
cwMzQyODQ3NSwxMjU3MTc5OTE1XX0=
-->