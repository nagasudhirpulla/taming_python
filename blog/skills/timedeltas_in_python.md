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
print('time1 = {0}'.format(t1.strftime('%d %b %Y %H:%M:%S')))

# t2 would be 15th June 2018
t2 = dt.datetime(2018, 6, 15)
print('time2 = {0}'.format(t2.strftime('%d %b %Y %H:%M:%S')))

# get the difference between the times as a timedelta object
tDiff = t1-t2
print('time1 - time2 = {0}'.format(tDiff))

# print the type of tDiff
print('type of tDiff = {0}'.format(type(tDiff)))
```
### add / subtract timeperiods to datetime using timedelta
time periods can be added/subtracted to datetime object using timedelta
```python
import datetime as dt

# get the current time
tNow = dt.datetime.now()
print('now = {0}'.format(tNow.strftime('%d %b %Y %H:%M:%S')))

# get datetime object after 15 hrs
tAfter15Hrs = tNow + dt.timedelta(hours = 15)
print('now + 15 hrs = {0}'.format(tAfter15Hrs.strftime('%d %b %Y %H:%M:%S')))

# get datetime object before 1 day, 3 weeks
tBefore = tNow - dt.timedelta(weeks = 3, days = 1)
print('now - 1 day, 3 weeks = {0}'.format(tBefore.strftime('%d %b %Y %H:%M:%S')))
```

### access timedelta components
```python
import datetime as dt

# create a timedelta object
tp = dt.datetime.now() - dt.datetime(2020,1,1)
print('timedelta object = {0}'.format(tp))
# print its compoenents
print('days = {0}'.format(tp.days))
print('seconds = {0}'.format(tp.seconds))
print('microseconds = {0}'.format(tp.microseconds))
```

### get the total timeperiod span in seconds using 'total_seconds' function
```python
import datetime as dt

# create a timedelta object
tDiff1May = dt.datetime.now() - dt.datetime(2020,1,1)

print('total timespan in seconds from 1st May 2020 = {0}'.format(tDiff1May.total_seconds()))
```

### Video
The video for this post can be seen [here](https://youtu.be/z-bUpe_FEt8)

<iframe width="560" height="315" src="https://www.youtube.com/embed/z-bUpe_FEt8" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/GraciousCourageousFirewall?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

<hr/>

### References
* Official documentation - https://docs.python.org/3/library/datetime.html#timedelta-objects
* another post - https://www.geeksforgeeks.org/python-datetime-timedelta-function/

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFRpbWVkZWx0YXMgaW4gcH
l0aG9uXG5hdXRob3I6IE5hZ3N1ZGhpciBQdWxsYVxuZGF0ZTog
JzIwMjAtMDUtMTEnXG50YWdzOiAnbGVhcm5pbmcsIHB5dGhvbi
wgdGFtaW5nX3B5dGhvbl9za2lsbCdcbmNhdGVnb3JpZXM6IHRh
bWluZ19weXRob25fc2tpbGxcbiIsImhpc3RvcnkiOlstMjEzNz
QxMzg0MiwtMzc3Nzk1ODQ1LC0yMTQ0MDIwNjY2LDE2ODk5NzMy
NzUsOTA2Mzc5MTg3LDE3MzE2MTcwMTldfQ==
-->