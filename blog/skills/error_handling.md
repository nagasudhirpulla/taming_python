## Skill - Handling errors in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post, we will learn to handle errors in our python programs

### Catching error using 'except'
```python
try:  
    # use mkdir function to create the folder
    print(int('a2'))  
except:  
    print('An error occured...')
```
In the above example, we used try except to catch the error

### Catching error using 'except' along with error information
```python
try:  
    # use mkdir function to create the folder
    print(int('a2'))  
except Exception as e:  
    print(e)
    # this prints
    # invalid literal for int() with base 10: 'a2'
```
In the above example, we catch the error in a variable `e` and print it

### Catch error based on the error type
```python
try:
  print(x)
except NameError:
  # handle if the error is of type `NameError`
  print("Name error occured, which means that, a variable name is not defined")
except OSError as err:
    # handle if the error is of type `OSError`
    print("OS error: {0}".format(err))
except:
  # handle any other error types
  print("Something else went wrong")

# the above program prints "Name error occured, which means that, a variable name is not defined"
```
In the above example, first we check if the error type is `NameError` and it.
Otherwise we check if the error is of type `OSError` and handle it.
After that  we catch any other types of errors.

### Using 'finally' keyword for must run code
```python
try:
  print(x)
except Exception as e:
  print("Error info: {0}".format(e))
finally:
  # using finally to run code regardless of errors in 'try' section
  print("This code runs regardless of errors")

# The above code prints
# Error info: name 'x' is not defined
# This code runs regardless of errors
```

### Create custom exception using 'raise'
```python
x = -2
if x < 0:
  raise Exception("Numbers less than zero are not allowed")
# the above code throws an error
```

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/FrenchEffectiveBash?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### References
* https://stackoverflow.com/questions/4990718/about-catching-any-exception
* https://www.w3schools.com/python/python_try_except.asp
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk4NjM3Mzg0LDEyMjkzMDMzNDJdfQ==
-->