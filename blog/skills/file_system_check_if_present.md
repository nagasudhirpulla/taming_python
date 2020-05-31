## Skill - Check if file or folder is present
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post, we will learn to check if a file or folder exists

### Check if a file exists using 'isfile' function
```python
# import the os.path module in order to use isdir function
import os.path

# specify the folder we desire to check
fPath = r'C:\Users\Nagasudhir\Documents\Python Projects\substation_pmu_dict_synthesis\index.py'

# use isdir function
isFolderPresent = os.path.isFile(fPath)
if isFolderPresent:
	print('File is present!!!')
else:
	print('File does not exist...')
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

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/DaringFastUser?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### References
* Official tutorial - https://pandas.pydata.org/pandas-docs/stable/getting_started/index.html
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc0NTY3ODkwLC0zNTM2NDYwMTAsNDMwMD
AyOTY2XX0=
-->