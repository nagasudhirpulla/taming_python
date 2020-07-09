## Skill - Boolean and Logical Operations on variables in Python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

### Main Code
Boolean means ```True``` or ```False```. For example
```python
x = False
y = True
```
In the above code the variable x is assigned a boolean value ```True``` and y is assigned a boolean value ```False```

#### == Operator 
* **==** comparison operator can be used to compare values on both sides and returns True only if both sides are equal. For example
```python
# assign value to variables
x = 10
y = 15

# this will print False
print(x==y)

# this will print True
print(x+5 == y)
```

#### not Operator
* **not** comparison operator will toggle a boolean value. For example
```python
# assign value to variables
x = True

# this will print False
print(not x)
print(not True)

# this will print False
y = not x
print(y)

# this will print True
print(not (1==2))
```

#### and Operator
* **and** comparison operator will give True only if both sides are ```True```. For example
```python
# this will print False
print(True and False)

# this will print True
print(True and True)

x = 10
y = 20

# this will print True
print(x==10 and y == 20)

# this will print False, since the left condition is False
print(x==300 and y == 20)
```

#### or Operator
* **or** comparison operator will give True if any of both sides are ```True```. For example
```python
# this will print True
print(True or False)

# this will print True
print(True or True)

# this will print False
print(False or False)

x = 10
y = 20

# this will print True
print(x==10 or y == 30)

"""
this will print False, 
since both left and right conditions are False
"""
print(x == 40 or y == 50)
```

#### Logical Operations
```python
x = 10
y = 15

# add x and y and then assign to z
z = x + y

# subtract x and y and then assign to z
z = x - y

# multiply x and y and then assign to z
z = x * y

# divide x and y and then assign to z
z = x / y

# compute y power 3 and then assign to z
z = y**3

# floored division, It will return the integer part of the division operation. Example: 10 // 4 = 2 , 15 // 6 = 2
z = x // y

# modulo operation, it will return the remainder of the division operation. Example 18 % 4 = 2, 13 % 3 = 1
z = x % y

# some other equation
z = 2*x + x**2 + 3*y
```

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/PlainLeftAttributes?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### Further Reading
* http://thomas-cokelaer.info/tutorials/python/boolean.html#booleans

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IE9wZXJhdGlvbnMgb24gVm
FyaWFibGVzIGluIFB5dGhvblxuYXV0aG9yOiBOYWdhc3VkaGly
IFB1bGxhXG50YWdzOiAnbGVhcm5pbmcsIHB5dGhvbiwgdGFtaW
5nX3B5dGhvbl9za2lsbCdcbmNhdGVnb3JpZXM6IHRhbWluZ19w
eXRob25fc2tpbGxcbmRhdGU6ICcyMDIwLTA0LTE1J1xuIiwiaG
lzdG9yeSI6Wzc5MjcyMjY3MywxNzMyMTc5NjgzLC0yMDYxMDg5
ODgzLDkzMDM0MjY5OSwxNTQ3OTAwNTA1LC0xNDc3MTk5MjQ0LC
0xNTY0NjQwNjg0LC0yMDA1NDM5NTQ2LC03ODM4NzcxNjEsLTE4
OTIwOTI3ODQsMjE0NDUyNjQzMV19
-->