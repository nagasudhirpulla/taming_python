## Skill - Create a sequence of numbers in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Lists in python](https://nagasudhir.blogspot.com/2020/04/lists-in-python.html)
* [Create sequences with range function in python](https://nagasudhir.blogspot.com/2020/05/create-sequences-with-range-function.html)
* [For loop in python](https://nagasudhir.blogspot.com/2020/05/for-loop-in-python.html)
* [List Comprehensions in python](https://nagasudhir.blogspot.com/2020/05/list-comprehensions-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will learn how to create sequence of numbers in python using three approaches

* using `range` function with syntax `range(start, stop, step)`
* using list comprehensions (which are one basically liners of a for loop)
* using `arrange` and `linspace` functions of numpy

These sequences of number can be used in for loops and many other situations

### Approach 1 - using range function
'range' is a python built-in **sequence generator** function through which we can generate sequences
#### Syntax
```
range(start, stop, step)
```
The post on how to use range function can be seen [here](https://nagasudhir.blogspot.com/2020/05/create-sequences-with-range-function.html)
#### 'range' function code example
```python
# create a sequence from 0 to 4, i.e., 0,1,2,3,4
x = range(5)

# create a sequence from 1 to 7, i.e., 1,2,3,4,5,6,7
x = range(1,8)

# sequence from 2 to 12 with steps of 2, i.e., 2,4,6,8,10,12
x = range(2,13,2)

# create a list from range using the * operator inside square brackets
y = [*x]
# Now y is a list which is derived from a range x
```

### Approach 2 - using list comprehensions
List Comprehensions can be used to create a list from another list/sequence in a user-friendly way and with less lines of code.
The post on how to use list comprehensions can be seen [here](https://nagasudhir.blogspot.com/2020/05/list-comprehensions-in-python.html)

#### list comprehension code example
```python
lst = [t for t in range(15)]

print(lst)
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]

# using filter in list comprehension to create a sequence of even numbers
lst = [x for x in range(0,17) if x%2==0]

print(lst)
# [0, 2, 4, 6, 8, 10, 12, 14, 16]
```

### Approach 3 - using numpy 'arange' and 'linspace' functions
This approach is very useful if you want to create sequence of decimal numbers
Make sure you have numpy module installed by typing the following in the command line
```
pip install numpy
```

#### numpy arange code example
Use arange function for creating a sequence with **fixed interval** between numbers (also called 'step')
The syntax is ```np.arange(start, stop, step)``` , `start` and `step` are optional
```python
# import the numpy module
import numpy as np

# only 'stop' input given to arange function
s = np.arange(5).tolist()

print(s)
# [0, 1, 2, 3, 4]

# 'start' and 'stop' input given to arange function
s = np.arange(1,6).tolist()
print(s)
# [1, 2, 3, 4, 5]

# 'start', 'stop', 'step' input given to arange function
s = np.arange(1,6, 0.5).tolist()
print(s)
# [1.0, 1.5, 2.0, 2.5, 3.0, 3.5, 4.0, 4.5, 5.0, 5.5]
```

#### numpy linspace code example
Use linspace function for creating a sequence with `fixed number of samples` from start to end
The syntax is ```np.linspace(start, stop, num)``` 
```python
# import the numpy module
import numpy as np

# get 15 evenly spaced numbers from 1 to 8 using linspace function
s = np.linspace(1,8,num=15).tolist()

print(s)
# [1.0, 1.5, 2.0, 2.5, 3.0, 3.5, 4.0, 4.5, 5.0, 5.5, 6.0, 6.5, 7.0, 7.5, 8.0]
```

### Video
Video for this post can be found [here](https://youtu.be/SKlf1DJUl0w)

<iframe width="560" height="315" src="https://www.youtube.com/embed/SKlf1DJUl0w" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

### References
* numpy linspace function - https://numpy.org/doc/stable/reference/generated/numpy.linspace.html#numpy.linspace
* numpy arrange function - https://numpy.org/doc/stable/reference/generated/numpy.arange.html
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoiYXV0aG9yOiBOYWdhc3VkaGlyIFB1bG
xhXG50YWdzOiAnbGVhcm5pbmcsIHB5dGhvbiwgdGFtaW5nX3B5
dGhvbl9za2lsbCdcbmNhdGVnb3JpZXM6IHRhbWluZ19weXRob2
5fc2tpbGxcbmRhdGU6ICcyMDIwLTA3LTA2J1xudGl0bGU6IENy
ZWF0ZSBhIHNlcXVlbmNlIG9mIG51bWJlcnMgaW4gcHl0aG9uXG
4iLCJoaXN0b3J5IjpbODA0MjM0Mjc3LDEwNzUyMjMxNzMsNDk4
ODcxNTU5LDY4ODI4NjM1NiwtODI1ODc3MjUzLDIwMTQ0OTU2NT
UsMTkwMDg1NzM4MCwxNjE4MjY1NTAsLTM4MjY0MTE5MCwtMTk1
MzQ5MTE2MSwtMTIyOTYwNjg1NF19
-->