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
# define a function that takes in radius as input and returns surface area
def compute_surface_area(radius):
    return 3.14 * radius * radius

# use the function by passing the required parameter
sa = compute_surface_area(5)
print(sa)
# this prints 78.5
```
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEZ1Y250aW9ucyBpbiBweX
Rob25cbmF1dGhvcjogTmFnYXN1ZGhpciBQdWxsYVxuZGF0ZTog
JzIwMjAtMDUtMjMnXG50YWdzOiAnbGVhcm5pbmcsIHB5dGhvbi
wgdGFtaW5nX3B5dGhvbl9za2lsbCdcbmNhdGVnb3JpZXM6IHRh
bWluZ19weXRob25fc2tpbGxcbiIsImhpc3RvcnkiOlsxMDYwOD
M0NThdfQ==
-->