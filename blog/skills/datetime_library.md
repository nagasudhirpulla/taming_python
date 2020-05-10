
## Skill - Dictionaries in Python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

`datetime` library in python is very useful in manipulating date-times.

### Installation
In command prompt type `pip install datetime` and press Enter

![pip install datetime image](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/pip_install_datetime.png)
### Create a datetime
```python
import datetime as dt

# get current time
curTime = dt.datetime.now()
print(curTime)

# create a datetime from a specific date time, say 10th May 2020 15 Hrs, 22 mins, 40 secs
t1 = dt.datetime(2020, 5, 10, 15, 22, 40)
print(t1)

# create a datetime from a specific date only, say 10th May 2020
t2 = dt.datetime(2020, 5, 10)
print(t2)

# create datetime from UNIX timestamp
# Unix 
```
As shown above it is really easy to create datetime objects

### convert string to datetime using 'strptime'




### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

### You can practice here


<hr/>

### References
* Detailed examples - https://www.programiz.com/python-programming/datetime
* Official documentation - https://docs.python.org/3/library/datetime.html

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IERhdGV0aW1lIGxpYnJhcn
kgaW4gcHl0aG9uXG5hdXRob3I6IE5hZ2FzdWRoaXIgUHVsbGFc
bmRhdGU6ICcyMDIwLTA1LTEwJ1xudGFnczogJ2xlYXJuaW5nLC
BweXRob24sIHRhbWluZ19weXRob25fc2tpbGwnXG5jYXRlZ29y
aWVzOiB0YW1pbmdfcHl0aG9uX3NraWxsXG4iLCJoaXN0b3J5Ij
pbMTIwOTIxMjA5NiwtMTg1NjYzMjgzNCw0NTkxNTAxMTQsMzg4
MjEzMTIxXX0=
-->