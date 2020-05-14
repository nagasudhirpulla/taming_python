## Skill - Lists in Python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

In this post we will try to learn how to generate random numbers using `random` module in python

### Create a random integer using 'randrange'
```python
import random

# create a random integer between 10 and 20
intNum = random.randrange(10,21)

print('random integer between 10 and 20 = {0}'.format(intNum))
```

### Create a random decimal value using 'uniform'
```python
import random

# create a random real value such that 10<=realNum<20
realNum = random.uniform(10,20)

print('random real number between 10 and 20 = {0}'.format(realNum))
```

### Example: create a list of 10 random numbers
```python
import random

realNums = []

# run a loop for 10 times
for p in range(10):
	realNUm

print('random real number between 10 and 20 = {0}'.format(realNum))
```

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

### You can practice here


<hr/>

### References
* https://docs.python.org/3/library/random.html#examples-and-recipes
* https://www.tutorialspoint.com/generating-random-number-list-in-python

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExMDIyODExNzhdfQ==
-->