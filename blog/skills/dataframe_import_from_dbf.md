## Skill - Filter DataFrame rows
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

In this post, we will learn how to filter the rows of a DataFrame based on our desired criteria

<hr/>

#### Instructions to run the codes below
* Create a folder and place the csv file used in this post from [here](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/gen_schedules.csv)
* Open the folder in Visual Studio Code
* Create and work on python files in this folder

The excel files should look like the image below 
![excel_file_illustration](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/all_gen_data.png)

Suppose in a DataFrame `df` we want to get rows with values in column 'A' greater than 20, then we use `df[df['A']>20]`

### Example
```python
# import pandas module
import pandas as pd
# import Dbf5 module from simpledbf module
from simpledbf import Dbf5

# path of dbf file
dbfPath = r'C:\Users\Nagasudhir\Documents\test.dbf'

df = dbf.to_dataframe(dbfPath)
```

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* https://stackoverflow.com/questions/41898561/pandas-transform-a-dbf-table-into-a-dataframe

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEltcG9ydCBwYW5kYXMgRG
F0YUZyYW1lIGZyb20gREJGIGZpbGVcbmF1dGhvcjogTmFnYXN1
ZGhpciBQdWxsYVxuZGF0ZTogJzIwMjAtMDYtMTgnXG50YWdzOi
AnbGVhcm5pbmcsIHB5dGhvbiwgdGFtaW5nX3B5dGhvbl9za2ls
bCdcbmNhdGVnb3JpZXM6IHRhbWluZ19weXRob25fc2tpbGxcbi
IsImhpc3RvcnkiOlstNjI0NTQ1MjU0XX0=
-->