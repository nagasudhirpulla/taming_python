
## Skill - 'any', 'all' keywords in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Boolean and Logical Operations on variables in Python](https://nagasudhir.blogspot.com/2020/04/operations-on-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

**any** keyword evaluates to True if any one item in the supplied list is True or 1. 
**any** is like applying an **or** statement over a list of items 
```python
x = True
y = False
z = False

k = any([x,y,z])
print(k) # True

k = any([False, False, False])
print(k) # False

k = any([0,0,1])
print(k) # True

k = any([0<5, 20>50, 40*2==80])
print(k) # True
```

**all** keyword evaluates to True only if all items in the supplied list is True or 1. 
**all** is like applying an **and** statement over a list of items 
```python
x = True
y = False
z = False

k = all([x,y,z]) 
print(k) # False

k = all([True, True, True]) 
print(k) # True

k = all([0,0,1])
print(k) # False

k = all([0<5, 20>50, 40*2==80])
print(k) # False
```

### Practical Example
```python
nums = [5,21,54,96,71]

# check if any one number is less than 10
k = [True if x<10 for x in nums]
print(k) # [True,False,False,False,False]

if any(k):
	print("Atleast one number is less than 10 in the list")

```

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY2OTUxNjE3NCwtMTkyNTM1NDk0NF19
-->