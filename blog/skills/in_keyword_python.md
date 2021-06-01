## Skill - 'in' keyword in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Lists in python](https://nagasudhir.blogspot.com/2020/04/lists-in-python.html)
* [Strings in python](https://nagasudhir.blogspot.com/2020/04/strings-in-python.html)
* [for loop in python](https://nagasudhir.blogspot.com/2020/05/for-loop-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

`in` keyword in python can be used to 
* check if an item is present in a collection like list, tuple, range, string
* iterate over a sequence like list, tuple, range etc using a for loop

### For loop on an array
```python
x = [1,8,6,5]
for n in x:
	print('The number is {0}'.format(n))

# this will print
# The number is 1
# The number is 8
# The number is 6
# The number is 5

y = ['Nagasudhir', 'Lakshmi', 'Kishore']
for n in y:
	print('Hi {0}!'.format(n))
# this will print
# Hi Nagasudhir!
# Hi Lakshmi!
# Hi Kishore!
```

### For loop on a sequence
In this example we are generating a sequence using range function
```python
for n in range(1,10,2):
	print('The number is {0}'.format(n))

# this will print
# The number is 1
# The number is 3
# The number is 5
# The number is 7
# The number is 9
```

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

### Video
The video for this post can be found [here](https://youtu.be/JqQPgGKzp9I)
<iframe width="560" height="315" src="https://www.youtube.com/embed/JqQPgGKzp9I" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>


### References
* https://www.geeksforgeeks.org/python-in-keyword/


<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUwOTM5NzQ3MywxNTcyMjczNzk2XX0=
-->