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

## Method #1 - 'rename' method for targeted columns
This method can be used if we want to rename less number of targeted columns
```python
# import pandas
import pandas as pd
# read csv
df = pd.read_csv("ramen-ratings.csv")

# rename targeted columns using rename method
df.rename(columns={"Review #": "review", "Top Ten":"top_ten"}, inplace=True) 

print(df.head())
```

## Method #2 - assign all column names at once
```python
import pandas as pd
# read csv
df = pd.read_csv("ramen-ratings.csv")

# get dataframe column names as a list
dfCols = df.columns.tolist()
print(dfCols)

# derive new column names from existing column names using a simple list comprehension
# In this case we are stripping off border whitespaces and replacing spaces with _
newCols = [str(x).strip().replace(" ", "_").lower() for  x  in  df.columns]
df.columns = newCols

# assign new column names as a list of strings
# length of new column names list should match the length of original columns list
newCols = ["revw", "brnd", "varty", "stl", "cntry", "strs", "tptn"]
df.columns = newCols
```

### Video
Video for this post can be found [here](https://youtu.be/iqy6IBxiL40)

<iframe width="560" height="315" src="https://www.youtube.com/embed/iqy6IBxiL40" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* Official guide - https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.rename.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU2NTYxMjgwOCwtMTg4NzYyMjU4MSwtMT
gzOTg2NDY4MiwxODA0NDI5MjM2LDExNjc0MDk0MzYsLTE3OTI4
Njk0OTYsLTE2NTAwOTgyNTYsLTE4NDUxNjI1MzRdfQ==
-->