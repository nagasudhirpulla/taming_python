## Skill - Create sequences with range function in python

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Lists in python](https://nagasudhir.blogspot.com/2020/04/lists-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

Range is a python built-in sequence generator function in python through which we can generate sequences

These sequences can be used in for loops and many other situations

### Syntax
```
range(start, stop, step)
```
here ```start``` and ```step``` are optional parameters
* start = optional input that specifies the number from which the sequence should start, default value is 0
* stop = input that specifies the number at which the sequence should end
* step = optional input that specifies the incrementation of sequence. default value is 1

### Generating a sequence
```python
# create a sequence from 0 to 4, i.e., 0,1,2,3,4
x = range(5)

# create a sequence from 1 to 7, i.e., 1,2,3,4,5,6,7
x = range(1,8)

# sequence from 2 to 12 with steps of 2, i.e., 2,4,6,8,10,12
x = range(2,13,2)
```

### Iterating over a sequence
Using `in` operator with `for` loop, we can iterate over a sequence
```python
# create sequence from 2 to 12 with steps of 2, i.e., 2,4,6,8,10,12
x = range(2,13,2)

# iterate over the sequence using for loop and in operator
for n in x:
	print(n)
# this code should print 2,4,6,8,10,12 in each line of the console
```

### Creating a list from sequence
```python
# create sequence from 2 to 12 with steps of 2, i.e., 2,4,6,8,10,12
x = range(2,13,2)

# create a list from sequence
y = [*x]

print(y)
# this code should print [2,4,6,8,10,12]
```


### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IENyZWF0ZSBzZXF1ZW5jZX
Mgd2l0aCByYW5nZSBmdW5jdGlvblxuYXV0aG9yOiBOYWdhc3Vk
aGlyIFB1bGxhXG50YWdzOiAnbGVhcm5pbmcsIHB5dGhvbiwgdG
FtaW5nX3B5dGhvbl9za2lsbCdcbmNhdGVnb3JpZXM6IHRhbWlu
Z19weXRob25fc2tpbGxcbmRhdGU6ICcyMDIwLTA1LTAyJ1xuIi
wiaGlzdG9yeSI6Wy0xNzAyMDczNDA3LDE5MTQyODU3NTBdfQ==

-->