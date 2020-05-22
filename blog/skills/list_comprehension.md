## Skill - List Comprehensions in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Lists in python](https://nagasudhir.blogspot.com/2020/04/lists-in-python.html)
* [Create sequences with range function in python](https://nagasudhir.blogspot.com/2020/05/create-sequences-with-range-function.html)
* ['for' loop in python](https://nagasudhir.blogspot.com/2020/05/for-loop-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

**List Comprehension** can be used to create a list from another list/sequence in a user-friendly way and with less lines of code. 
All List comprehension can be replaced by a `for` loop.
But all `for` loops can't be replaced by List comprehensions.



### Creating a list of 15 numbers using 'List Comprehension'
```python
lst = [t for t in range(15)]

print(lst)
# This will print
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]
```
### Creating a list of 15 numbers using 'for' loop
```python
lst = []

for t in range(15):
	lst.append(t)

print(lst)
# This will print
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]
```

You can see from the above two examples that list comprehension is more user friendly to write and uses less lines of code

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

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/LimeWiltedRouter?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IExpc3QgY29tcHJlaGVuc2
lvbnMgaW4gcHl0aG9uXG5hdXRob3I6IE5hZ2FzdWRoaXIgUHVs
bGFcbmRhdGU6ICcyMDIwLTA1LTIyJ1xudGFnczogJ2xlYXJuaW
5nLCBweXRob24sIHRhbWluZ19weXRob25fc2tpbGwnXG5jYXRl
Z29yaWVzOiB0YW1pbmdfcHl0aG9uX3NraWxsXG4iLCJoaXN0b3
J5IjpbLTEzMTc5NjMwNjEsNTkxMTE2MTUzLC0zMzQ0Nzk2OTVd
fQ==
-->