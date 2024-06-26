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
Generally people use list comprehensions write simple for loops in a single line
All List comprehensions can be replaced by a `for` loop.
But all `for` loops can't be replaced by List comprehensions.

### Creating list from another sequence/list using list comprehension
![list_comprehension_illustration](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/list_comprehension_illustration.png)
* As shown in the above image, for creating a new list we require the input list, operation on each list item, conditional statement for including the list item if any.
* The conditional statement can be used as a `filter` to exclude undesired list items from the output list 

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

### Converting all strings in list to uppercase
```python
cities = ['Mumbai', 'Delhi', 'Bangalore ', 'Hyderabad',
          'Ahmedabad', 'Chennai', 'Kolkata',
          'Surat', 'Pune']

lst = [x.upper() for x in cities]

print(lst)
```

### Using the conditional statement as filter in list comprehension
In this example we will generate even numbers using list comprehension
```python
lst = [x for x in range(0,17) if x%2==0]

print(lst)
# this will print
# [0, 2, 4, 6, 8, 10, 12, 14, 16]
```

### Video
Video for this post can be found [here](https://youtu.be/8pkY377lVqE)

<iframe width="560" height="315" src="https://www.youtube.com/embed/8pkY377lVqE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IExpc3QgY29tcHJlaGVuc2
lvbnMgaW4gcHl0aG9uXG5hdXRob3I6IE5hZ2FzdWRoaXIgUHVs
bGFcbmRhdGU6ICcyMDIwLTA1LTIyJ1xudGFnczogJ2xlYXJuaW
5nLCBweXRob24sIHRhbWluZ19weXRob25fc2tpbGwnXG5jYXRl
Z29yaWVzOiB0YW1pbmdfcHl0aG9uX3NraWxsXG4iLCJoaXN0b3
J5IjpbLTE4Mzk2NzIxMTEsLTE1MzUyMTkyMjEsLTIzOTg3MTg5
NywtNTQ2MjUzNjY0LDU5MTExNjE1MywtMzM0NDc5Njk1XX0=
-->