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

### 'in' with if condition
```python
names = ['john', 'smith', 'tom', 'Harry']
for k in names:
	print('The name is {0}'.format(k))

for n in range(5):
	print(n)
```

### 'in' with for loop
```python
names = ['john', 'smith', 'tom', 'Harry']

if 'smith' in names:
	print('smith is in the list!')

isTomPresent = 'tom' in names
print(isTomPresent) # True

isHPresent = 'H' in 'Harry'
print(isTomPresent) # True
```


<hr/>

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

### References
* https://www.geeksforgeeks.org/python-in-keyword/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMzM3ODY5ODgsMTExMTU4MDk4MSwxNT
cyMjczNzk2XX0=
-->