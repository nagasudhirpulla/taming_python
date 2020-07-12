## Skill - 'if', 'else' and 'elif' in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Boolean and Logical Operations on variables in Python](https://nagasudhir.blogspot.com/2020/04/operations-on-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* **if** condition runs a code only if the supplied expression evaluates to ```True```. For Example
```python
x = 5
# the print statement will execute since x is 5
if x==5:	
	print('The value of x is 5')

# the print statement will not execute since x is not 10
if x==10:
	print('The value of x is 10')
```
* **else** can be used to execute when if condition is supplied with value that evaluates to false. For example
```python
x=10
if x==5:	
	print('The value of x is 5')
else:
	print('The value of x is not 5')
```
* **elif** keyword is used to implement else-if in python. For example
```python
x = 9

if x==2:
	print('The value of x is 2')
elif x==3:
	print('The value of x is 3')
elif x==4:
	print('The value of x is 4')
elif (x>4) and (x<10):
	print('x is greater than 4 and less than 10')
else:
	print('x is greater than 10')
```
* if, else, elif can be nested with in each of them to suit our requirements, for example
```python
age = 28
country = 'India'

if country=='India':
	if age<=25:
		print('logic for country as India and age less than or equal to 25')
		print('Executing some application logic...')
	elif age<60:
		print('logic for country as India and age more than 25 and age less than 60')
		print('Executing some application logic...')
	else:
		print('logic for country as India and age greater than or equal to 60')
		print('Executing some application logic...')
```

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/GregariousInexperiencedLinuxpc?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### Further Reading
* https://docs.python.org/3.8/tutorial/controlflow.html#if-statements

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IGlmIENvbmRpdGlvbiBpbi
BweXRob25cbmF1dGhvcjogTmFnYXN1ZGhpciBQdWxsYVxuZGF0
ZTogJzIwMjAtMDQtMTUnXG50YWdzOiAncHl0aG9uLCBsZWFybm
luZywgdHV0b3JpYWwsIHRhbWluZ19weXRob25fc2tpbGwnXG5j
YXRlZ29yaWVzOiB0YW1pbmdfcHl0aG9uX3NraWxsXG4iLCJoaX
N0b3J5IjpbOTQ5NjMxNzAyLC0xMTUzMzMzODEyLDQ4ODA3Mjgy
NCw3MjQxODcwNjldfQ==
-->