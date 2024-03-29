## Skill - Boolean and Arithmetic Operations on variables in Python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr>

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
print((x==10) and (y == 20))

# this will print False, since the left condition is False
print((x==300) and (y == 20))
```

#### <, <=, >, >= Operators
The following are some important comparison operators for inequality equations
* `>` is 'greater than' operator
* `>=` is 'greater than or equal to' operator
* `<` is 'less than' operator
* `<=` is 'less than or equal to' operator

```python
x = 10
y = 20

# this will print False
print((x > y))

# this will print True
print((x < y))

# this will print True
print((x <= y-10))

# this will print True
print((x+10 >= y))
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
print((x==10) or (y == 30))

"""
this will print False, 
since both left and right conditions are False
"""
print((x == 40) or (y == 50))
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

# calculating an arithmetic equation and storing in a variable
z = 2*x + x**2 + 3*y
```

#### Calculating an arithmetic equation
```python
# calculating an arithmetic equation and storing in a variable
x = 10
y = 20

z = 2*x + x**2 + 3*y

print('The value of z =', end=' ')
print(z)
# this will print 180
```

#### Combining both comparison and arithmetic operators
```python
# calculating an arithmetic equation and storing in a variable
x = 10
y = 20
z = 30

k = ( (2*x + x**2 + 3*y) > 4*z )

print('The value of k is', end=' ')
print(z)
# this will print True
```

### Video
The video on this post can be found [here](https://youtu.be/kwsLop-mW3M)

<iframe width="560" height="315" src="https://www.youtube.com/embed/kwsLop-mW3M" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

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
lzdG9yeSI6WzEyMTkyOTkxOTUsLTE2NDU5Mjc2MTUsOTg0NDkx
MDI3LDE2MTc4MzUwMDksMzI4MjU0NTcyLC0xMjE4NzU4MDEsNz
kyNzIyNjczLDE3MzIxNzk2ODMsLTIwNjEwODk4ODMsOTMwMzQy
Njk5LDE1NDc5MDA1MDUsLTE0NzcxOTkyNDQsLTE1NjQ2NDA2OD
QsLTIwMDU0Mzk1NDYsLTc4Mzg3NzE2MSwtMTg5MjA5Mjc4NCwy
MTQ0NTI2NDMxXX0=
-->