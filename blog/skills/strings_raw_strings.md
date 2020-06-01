## Skill - raw strings in Python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [strings in python](https://nagasudhir.blogspot.com/2020/04/strings-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

while declaring a string, the `\` character is treated as an escape character, hence to incorporate `\` in our strings, we have to write `\\`. 
To avoid this we can use raw strings as shown below

### Code
```python
# without using raw strings
x = 'Hi\nSudhir\n'
print(x)
# This will print
# Hi
# Sudhir

# using raw strings
y = r'Hi\nSudhir\n'
print(y)
# This will print
# Hi\nSudhir\n
# Notice that \n is used as it is, since we used 'r' before string declaration

# without using raw strings
z = 'C:\\Users\\Nagasudhir\\Documents\\Static_Web_Projects\\WRLDC Apps Dashboard'
print(z)
# This will print
# 'C:\Users\Nagasudhir\Documents\Static_Web_Projects\WRLDC Apps Dashboard'
# Notice that we had to use \\ in order to print \

# using raw strings
k = r'C:\Users\Nagasudhir\Documents\Static_Web_Projects\WRLDC Apps Dashboard'
print(k)
# This will print
# 'C:\Users\Nagasudhir\Documents\Static_Web_Projects\WRLDC Apps Dashboard'
# Notice that we need not use \\ since we used 'r' before string declaration

```

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/DifficultBowedOrigin?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFJhdyBzdHJpbmdzIGluIH
B5dGhvblxuYXV0aG9yOiBOYWdhc3VkaGlyIFB1bGxhXG50YWdz
OiAnbGVhcm5pbmcsIHB5dGhvbiwgdGFtaW5nX3B5dGhvbl9za2
lsbCdcbmNhdGVnb3JpZXM6IHRhbWluZ19weXRob25fc2tpbGxc
bmRhdGU6ICcyMDIwLTA2LTAxJ1xuIiwiaGlzdG9yeSI6Wy01NT
U4OTM3MTZdfQ==
-->