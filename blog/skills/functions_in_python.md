## Skill - Functions in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup Python Development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Commenting in python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Basic printing in python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

Functions can be used to encapsulate logic so that we can get an output for a given input based on the function's logic
The  pictorial representation can be as shown below

![function_illustration](https://raw.githubusercontent.com/nagasudhirpulla/taming_python/master/blog/skills/assets/img/function_illustration.png)

### Structure of a function in python
![python_function](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/python_function.png)

### Function example in python
```python
# define a function that adds 2 numbers
def add(x,y):
    return x+y

# use the function by passing the required parameter
sum = add(5, 6)
print(sum)
# this prints 11
```

### Function with optional and named parameters
```python
# define a function that adds 2 numbers
def multiply(x,y=1):
    return x*y

# since we didn't give second input, it is considered 
# as the default value, i.e., 1
a = multiply(15)
print(a)
# this prints 15

# here we are giving both the inputs
b = multiply(15, 2)
print(b)
# this prints 30

# we can also give inputs through input variable names
c = multiply(x=12, y=4)
print(c)
# this prints 48
```

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/ or https://repl.it/repls/MountainousWhirlwindRatios

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/RelievedParallelAnalysts?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### References
* http://thomas-cokelaer.info/tutorials/python/functions.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEZ1Y250aW9ucyBpbiBweX
Rob25cbmF1dGhvcjogTmFnYXN1ZGhpciBQdWxsYVxuZGF0ZTog
JzIwMjAtMDUtMjMnXG50YWdzOiAnbGVhcm5pbmcsIHB5dGhvbi
wgdGFtaW5nX3B5dGhvbl9za2lsbCdcbmNhdGVnb3JpZXM6IHRh
bWluZ19weXRob25fc2tpbGxcbiIsImhpc3RvcnkiOlsxNTAyNT
k2NDIyLDE0NTEwODI4NTZdfQ==
-->