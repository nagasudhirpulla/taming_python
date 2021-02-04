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
In this post, we will learn how to import dataframe from a `dbf` file

In order to import dataframe from dbf file, we require simpledbf module.
Install simpledbf using the command `pip install simpledbf`

### Example
```python
# import pandas module
import pandas as pd
# import Dbf5 module from simpledbf module
from simpledbf import Dbf5

# path of dbf file
dbfPath = r'C:\Users\Nagasudhir\Documents\test.dbf'

# load the dataframe from dbf file path
df = dbf5.to_dataframe(dbfPath)
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
IsImhpc3RvcnkiOls0NTIzNTA2MDUsLTE4NjA4ODI5NTIsLTEy
NTMzNDE0NDJdfQ==
-->