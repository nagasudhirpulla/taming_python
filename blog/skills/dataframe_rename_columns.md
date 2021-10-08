## Skill - Rename columns of a Pandas DataFrame
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

In this post we will learn how to rename the columns of a Pandas Dataframe

The data file used in this post can be downloaded [here](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/ramen-ratings.csv)

## call 'rename' method on a dataframe
This method can be used if we want to rename very less number of targeted columns
```python
# import pandas
import pandas as pd
# read csv
df = pd.read_csv('ramen-ratings.csv')


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
eyJoaXN0b3J5IjpbLTQ0ODYxMzExNSwtMTY1MDA5ODI1NiwtMT
g0NTE2MjUzNF19
-->