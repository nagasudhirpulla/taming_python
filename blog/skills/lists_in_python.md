## Skill - Lists in Python

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

Lists means just a list of objects

### Main Code
#### Basic stuff
```python
# creating a list and storing in variable x
x = [0,2,4,5,9]

# print the first element (index=0)
print(x[0])
# print the third element (index=2)
print(x[2])

# print length of the list using len function
print(len(x))
```

#### "append" function to add new elements at the end
```python
# create a list
x = [1,5,3,7,4]

# add 10 at the end of the list
x.append(10)
# add 15 at the end of the list
x.append(15)

# print to verify that 10, 15 are added at the end
print(x)
# this prints [1,5,3,7,4,10,15]
```

#### "extend" function to add multiple new elements at the end
```python
# create a list
x = [1,5,3,7,4]

# add numbers 10, 15 at the end of the list
x.extend([10, 15])

# print to verify that 10, 15 are added at the end
print(x)
# this prints [1,5,3,7,4,10,15]
```

#### "insert" function to add new element at any position
```python
# create a list
x = [1,5,3,7,4]

# add number 54 at the start the list
x.insert(0, 54)

# add number 21 at the second last position of the list
x.insert(len(x)-1, 21)

# print to verify that 54, 21 are added at the correct positions
print(x)
# this prints [54, 1, 5, 3, 7, 21, 4]
```

#### "index" function to search for the first occurrence in the list
```python
# initialize a list
x = ['a','b','c','b', 'a']

# find the position of 'b'
print(x.index('b'))
# prints 1

# find the position of 'b', but search from index 2
print(x.index('b', 2))
# prints 3
```
#### "sort" function to sort a list
```python
x = [5,1,2,9,4,6]
x.sort()
print(x)
# prints [1, 2, 4, 5, 6, 9]

x = ['z','w','p','a']
x.sort()
print(x)
# prints ['a', 'p', 'w', 'z']
```

#### "reverse" function
```python
x = [4,6,3,7,9]
x.reverse()
print(x)
# prints [9, 7, 3, 6, 4]
```

#### slicing a list using : operator
```python
x = [0, 1, 2, 3, 4, 5]

# get elements from index 2 
# prints [9, 7, 3, 6, 4]
```

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IExpc3RzIGluIFB5dGhvbl
xuYXV0aG9yOiBOYWdhc3VkaGlyIFB1bGxhXG50YWdzOiAnbGVh
cm5pbmcsIHB5dGhvbiwgdGFtaW5nX3B5dGhvbl9za2lsbCdcbm
NhdGVnb3JpZXM6IHRhbWluZ19weXRob25fc2tpbGxcbmRhdGU6
ICcyMDIwLTA1LTAxJ1xuIiwiaGlzdG9yeSI6Wy0yMDM0NjE2OD
IwLC0yOTExNjQ4NDMsLTIwNjA1NzI3NjIsLTIwMTU3NjQwNzIs
LTU3MDcxMDk3OSwtMTU3NzU4Mjc5MCwtMTE1Mzg2ODk2OV19
-->