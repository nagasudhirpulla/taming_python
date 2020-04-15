## Skill - Boolean and Logical Operations on variables in Python

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to go through all the skills mentioned above to understand and execute the code mentioned below

### Main Code
Boolean means ```True/False```. For example
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

# this will print False, since the lef condition is False
print(x == 40 and y == 50)
```
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IE9wZXJhdGlvbnMgb24gVm
FyaWFibGVzIGluIFB5dGhvblxuYXV0aG9yOiBOYWdhc3VkaGly
IFB1bGxhXG50YWdzOiAnbGVhcm5pbmcsIHB5dGhvbiwgdGFtaW
5nX3B5dGhvbl9za2lsbCdcbmNhdGVnb3JpZXM6IHRhbWluZ19w
eXRob25fc2tpbGxcbmRhdGU6ICcyMDIwLTA0LTE1J1xuIiwiaG
lzdG9yeSI6Wy04MTM5MDY1NDUsLTIwMDU0Mzk1NDYsLTc4Mzg3
NzE2MSwtMTg5MjA5Mjc4NCwyMTQ0NTI2NDMxXX0=
-->