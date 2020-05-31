## Skill - Creating a folder in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post, we will learn to create a folder using `mkdir` and `mkdirs` function

### Create a folder using 'mkdir' function
```python
# import the os module in order to use mkdir function
import os

# specify the file we desire to check
fPath = r'C:\Users\Nagasudhir\Documents\Python Projects'

try:  
    # use mkdir function to create the folder
    os.mkdir(fPath)  
except Exception as e:  
    print(e)
```

### Check if a folder exists using 'isdir' function
```python
# import the os.path module in order to use isdir function
import os.path

# specify the folder we desire to check
fPath = r'C:\Users\Nagasudhir\Documents\Python Projects'

# use isdir function
isFolderPresent = os.path.isdir(fPath)
if isFolderPresent:
	print('Folder is present!!!')
else:
	print('Folder does not exist...')
```

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* https://www.geeksforgeeks.org/python-check-if-a-file-or-directory-exists-2/
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNDY4MzY3MzgsMTE1Njc5ODYxNCwxNj
I3MDYyMTg0XX0=
-->