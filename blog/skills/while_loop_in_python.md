## Skill - while statement for looping in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

`while` statement is used to run code again and again until a specified condition is satisfied. 

### Using while statement to print 10 times
```python
x = 1
while x<=10:
	print('{0} - Hello World!'.format(x))
	x = x + 1
# this prints
'''
1 - Hello World!
2 - Hello World!
3 - Hello World!
4 - Hello World!
5 - Hello World!
6 - Hello World!
7 - Hello World!
8 - Hello World!
9 - Hello World!
10 - Hello World!
'''
```
### Using 'break' to abort while loop
In the example below, we can see that the loop is broken using the `break` keyword
```python
x = 1
while x<=10:
	print('{0} - Hello World!'.format(x))
	if x==4:
		break
	x = x + 1
# this prints
'''
1 - Hello World!
2 - Hello World!
3 - Hello World!
4 - Hello World!
'''
```

### Using 'continue' to skip iteration
In the example below, we can see that the loop is broken using the `break` keyword
```python
x = 1
while x<=10:
	if x==4:
		continue
	print('{0} - Hello World!'.format(x))
	x = x + 1
# this prints
'''
1 - Hello World!
2 - Hello World!
3 - Hello World!
4 - Hello World!
'''
```

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/IndelibleFineExperiment?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFdoaWxlIGxvb3AgaW4gcH
l0aG9uXG5hdXRob3I6IE5hZ2FzdWRoaXIgUHVsbGFcbnRhZ3M6
ICdsZWFybmluZywgcHl0aG9uLCB0YW1pbmdfcHl0aG9uX3NraW
xsJ1xuY2F0ZWdvcmllczogdGFtaW5nX3B5dGhvbl9za2lsbFxu
ZGF0ZTogJzIwMjAtMDUtMDMnXG4iLCJoaXN0b3J5IjpbLTkxMz
I3OTA1MSwxMzE0ODA5MDM2XX0=
-->