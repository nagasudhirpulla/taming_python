## Skill - Read and process pandas dataframes from large files using chunks
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Pandas DataFrame Basics](https://nagasudhir.blogspot.com/2020/05/pandas-dataframe-basics.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>
In this post, we will learn how to process dataframes from large csv and dbf files

If we desire to import dataframe from dbf file, we require simpledbf module.
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
df = Dbf5(dbfPath).to_dataframe()
```
The file used in this example can be downloaded from [here](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/marks.dbf)

### Video
Video for this post can be found [here](https://youtu.be/mRDpAQrb5cw)

<iframe width="560" height="315" src="https://www.youtube.com/embed/mRDpAQrb5cw" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* https://stackoverflow.com/questions/41898561/pandas-transform-a-dbf-table-into-a-dataframe

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3OTg1NzUyNTFdfQ==
-->