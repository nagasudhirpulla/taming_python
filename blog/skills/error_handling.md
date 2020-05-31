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

### Handling any error using 'except'
```python
try:  
    # use mkdir function to create the folder
    print(int('a2'))  
except:  
    print('An error occured...')
```
In the above example, we used try except to catch the error

### Create a folder with intermediate folders using 'makedirs' function
If we want to create intermediate folders also while creating a folder, use `makedirs` function
```python
import os

# specify the file we desire to check
fPath = r'C:\Users\Nagasudhir\Documents\Python Projects'

# use makedirs function to create the folder along
# with intermediate folders if required
os.makedirs(fPath, exist_ok=True)
```
by using `exist_ok=True`, exception will not be thrown if folder already exists

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* https://stackoverflow.com/questions/4990718/about-catching-any-exception
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3MDU1MzM4MDQsMTIyOTMwMzM0Ml19
-->