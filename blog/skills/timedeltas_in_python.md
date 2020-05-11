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
```python

```
As shown above it is really easy to create variable that can store time period using `timedelta` objects

### timedelta from difference of datetimes
timedelta can also be created as a difference between datetime objects
```python

```
### add / subtract timeperiods tp 
```python
import datetime as dt

dt1 = dt.datetime.now()
# convert datetime object to string using strftime
dtStr = dt.datetime.strftime(dt1, '%d %b %Y %H:%M:%S')
print(dtStr)
```

### access datetime components
```python
t1 = dt.datetime.now()

print('original object = {0}'.format(t1))
print('day = {0}'.format(t1.day))
print('month = {0}'.format(t1.month))
print('year = {0}'.format(t1.year))
print('hours = {0}'.format(t1.hour))
print('minutes = {0}'.format(t1.minute))
print('seconds = {0}'.format(t1.second))
print('microseconds = {0}'.format(t1.microsecond))
```


### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/VisibleLimitedKeyboardmacro?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

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
bWluZ19weXRob25fc2tpbGxcbiIsImhpc3RvcnkiOlstMTc4Nz
Q1MTMxMyw5MDYzNzkxODcsMTczMTYxNzAxOV19
-->