## Skill - Create random numbers in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

In this post we will try to learn how to generate random numbers using `random` module in python

### Create a random integer using 'randint'
```python
import random

# create a random integer between 10 and 20
intNum = random.randint(10,20)

print('random integer between 10 and 20 = {0}'.format(intNum))
```

### Create a random decimal value using 'uniform'
```python
import random

# create a random real value such that 10<=realNum<=20
realNum = random.uniform(10,20)

print('random real number between 10 and 20 = {0}'.format(realNum))
```

### Example: create a list of random numbers
```python
import random

realNums = []

# run a loop for 15 times
for p in range(15):
	realNums.append(random.randint(200,500))

print('fifteen random integers between 200 and 500 = {0}'.format(realNums))

lst = [random.uniform(10,60) for k in range(4)]
print('10 random decimal numbers between 10 and 60 are {0}'.format(lst))
```

### Video

You can the video on this post [here](https://youtu.be/Tm5bRKhy93c)

<iframe width="560" height="315" src="https://www.youtube.com/embed/Tm5bRKhy93c" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<hr/>

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/MistyroseFelineUsers?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### References
* https://docs.python.org/3/library/random.html#examples-and-recipes
* random.randint documentation- https://docs.python.org/3/library/random.html#random.randint
* random.uniform documentation - https://docs.python.org/3/library/random.html#random.uniform
* https://www.tutorialspoint.com/generating-random-number-list-in-python

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IENyZWF0ZSByYW5kb20gbn
VtYmVycyBpbiBweXRob25cbmF1dGhvcjogTmFnYXN1ZGhpciBQ
dWxsYVxudGFnczogJ3B5dGhvbiwgbGVhcm5pbmcsIHR1dG9yaW
FsLCB0YW1pbmdfcHl0aG9uX3NraWxsJ1xuY2F0ZWdvcmllczog
dGFtaW5nX3B5dGhvbl9za2lsbFxuZGF0ZTogJzIwMjAtMDUtMT
QnXG4iLCJoaXN0b3J5IjpbLTk3MTIxNTQxNiw0NjEzOTc1NzZd
fQ==
-->