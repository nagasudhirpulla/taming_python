## Skill - Managing time periods using 'timedelta' in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [strings in python](https://nagasudhir.blogspot.com/2020/04/strings-in-python.html)
* [Datetime library in python](https://nagasudhir.blogspot.com/2020/05/datetime-library-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

`datetime` library in python is very useful in manipulating date-times.
`timedelta` module is present in datetime library itself

### Installation
In command prompt type `pip install datetime` and press Enter

![pip install datetime image](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/pip_install_datetime.png)
### Create a time period object using timedelta
As shown below the `timedelta` function from datetime module can be used to create timedelta objects
```
dt.timedelta(days=0, seconds=0, microseconds=0, milliseconds=0,
 minutes=0, hours=0, weeks=0)
```
Example code is shown below
```python
import datetime as dt

# create timedelta object to represent a time period of 10days, 3 hours, 4 mins, 26 seconds
tDelta = dt.timedelta(days=10, hours=3, minutes=4, seconds=26)

print(tDelta)
```
As shown above it is really easy to create variable that can store time period using `timedelta` objects

### timedelta from difference of datetimes
timedelta can also be created as a difference between datetime objects
```python
import datetime as dt

# t1 would be 1st May 2020
t1 = dt.datetime(2020, 5, 1)
print('time1 = {}')

# t2 would be 15th June 2018
t2 = dt.datetime(2018, 6, 15)
```
### add / subtract timeperiods to datetime using timedelta
time periods can be added/subtracted to datetime object using timedelta
```python

```

### access timedelta components
```python

```

### get the total timeperiod span in seconds
```python

```

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

### You can practice here


<hr/>

### References
* Official documentation - https://docs.python.org/3/library/datetime.html#timedelta-objects
* 

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFRpbWVkZWx0YXMgaW4gcH
l0aG9uXG5hdXRob3I6IE5hZ3N1ZGhpciBQdWxsYVxuZGF0ZTog
JzIwMjAtMDUtMTEnXG50YWdzOiAnbGVhcm5pbmcsIHB5dGhvbi
wgdGFtaW5nX3B5dGhvbl9za2lsbCdcbmNhdGVnb3JpZXM6IHRh
bWluZ19weXRob25fc2tpbGxcbiIsImhpc3RvcnkiOlstNTc3Nz
AzODgzLDE2ODk5NzMyNzUsOTA2Mzc5MTg3LDE3MzE2MTcwMTld
fQ==
-->