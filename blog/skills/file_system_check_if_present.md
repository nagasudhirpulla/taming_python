## Skill - Check if file or folder is present
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [strings in python](https://nagasudhir.blogspot.com/2020/04/strings-in-python.html)
* [raw strings in python](https://nagasudhir.blogspot.com/2020/05/raw-strings-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post, we will learn to check if a file or folder exists

### Check if a file exists using 'isfile' function
```python
# import the os.path module in order to use isfile function
import os.path

# specify the file we desire to check
fPath = r'C:\Users\Nagasudhir\Documents\Python Projects\substation_pmu_dict_synthesis\index.py'

# use isfile function
isFilePresent = os.path.isfile(fPath)
if isFilePresent:
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
### Video
The video for this post can be seen [here](https://youtu.be/_HhobaIr3fY)

<iframe width="560" height="315" src="https://www.youtube.com/embed/_HhobaIr3fY" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* https://www.geeksforgeeks.org/python-check-if-a-file-or-directory-exists-2/
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IENoZWNrIGlmIGZpbGUgb3
IgZm9sZGVyIGlzIHByZXNlbnRcbmF1dGhvcjogTmFnYXN1ZGhp
ciBQdWxsYVxuZGF0ZTogJzIwMjAtMDUtMzEnXG50YWdzOiAnbG
Vhcm5pbmcsIHB5dGhvbiwgdGFtaW5nX3B5dGhvbl9za2lsbCdc
bmNhdGVnb3JpZXM6IHRhbWluZ19weXRob25fc2tpbGxcbiIsIm
hpc3RvcnkiOls2OTA0NDczMzgsMTk1NTI0ODM5NSwtNTYwNTY3
MTcyLC0xNDkxMTU4ODY5LC0zNTM2NDYwMTAsNDMwMDAyOTY2XX
0=
-->