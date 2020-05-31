## Skill - Delete a file or folder in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Handling errors in python](https://nagasudhir.blogspot.com/2020/05/hnadling-errors-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post, we will learn to delete a file or folder in python using `remove` and `rmdir` functions

### Delete a file using 'remove' function
```python
# import the os module in order to use mkdir function
import os

# specify the file we desire to delete
fPath = r'C:\Users\Nagasudhir\Documents\test.txt'

# check if the file exists first
fileExists = os.path.exists(fPath)

if fileExists:
    # use remove function to delete the file if it exists
    os.remove(fPath)  
else:  
    print("File does not exist")
```
We checked if the file exists at first because, `remove` function will raise an error if the desired file does not exist

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
* https://thispointer.com/python-how-to-remove-a-file-if-exists-and-handle-errors-os-remove-os-ulink/
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMxNjA4MDg0Nl19
-->