## Skill - Split a time interval using pandas date_range

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Pandas DataFrame Basics](https://nagasudhir.blogspot.com/2020/05/pandas-dataframe-basics.html)
* [datetime module in Python](https://nagasudhir.blogspot.com/2020/05/datetime-library-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

pandas ```date_range``` function can be used to split a time range based on a variety of frequency options


### split time interval by a specified time period
use the ```freq``` parameter of ```date_range``` function
```python
import pandas as pd
import datetime as dt

startDt = dt.datetime(2020,1,1)
endDt = dt.datetime(2020,1,20)

splitDates = pd.date_range(startDt, endDt, freq='D').tolist()
print(splitDates)

splitDates = pd.date_range(startDt, endDt, freq=dt.timedelta(days=3)).tolist()
print(splitDates)
```

### split time interval into a fixed number of intervals
use the ```periods``` parameter of ```date_range``` function
```python
import pandas as pd
import datetime as dt

startDt = dt.datetime(2020,1,1)
endDt = dt.datetime(2020,1,20)

splitDates = pd.date_range(startDt, endDt, periods=15).tolist()
print(splitDates)
```

### Video
You can the video on this post [here](https://youtu.be/tYKlLzAyv0Y)

<iframe width="560" height="315" src="https://www.youtube.com/embed/tYKlLzAyv0Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* Official docs- https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.date_range.html
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTkxNTk0NTU1LDUzNTIzNTEwMywxMTkyMD
Q4MTk1LDE1ODUzMzQ3MDRdfQ==
-->