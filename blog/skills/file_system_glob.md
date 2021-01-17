## Skill - iterate through files inside folder
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [strings in python](https://nagasudhir.blogspot.com/2020/04/strings-in-python.html)
* [raw strings in python](https://nagasudhir.blogspot.com/2020/05/raw-strings-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post, we will learn to iterate through files in a folder using `glob` module

### get all filenames in a folder
```python
# import the glob module
import glob

# specify the file we desire to delete
fPath = r'C:\Users\Nagasudhir\Documents\Static_Web_Projects\WRLDC Apps Dashboard'

# use glob to get the filenames of files in the folder
fNames = glob.glob(r'{0}\*'.format(fPath))

print(fNames)
'''
this will print
['C:\\Users\\Nagasudhir\\Documents\\Static_Web_Projects\\WRLDC Apps Dashboard\\assets', 
'C:\\Users\\Nagasudhir\\Documents\\Static_Web_Projects\\WRLDC Apps Dashboard\\cards.css', 
'C:\\Users\\Nagasudhir\\Documents\\Static_Web_Projects\\WRLDC Apps Dashboard\\cards.html', 
'C:\\Users\\Nagasudhir\\Documents\\Static_Web_Projects\\WRLDC Apps Dashboard\\index.css', 
'C:\\Users\\Nagasudhir\\Documents\\Static_Web_Projects\\WRLDC Apps Dashboard\\index.html', 
'C:\\Users\\Nagasudhir\\Documents\\Static_Web_Projects\\WRLDC Apps Dashboard\\index.js']
'''
```
As seen above, the full path of filenames will be returned.

### get all filenames with a desired extension using pattern matching
here we are using pattern matching to filter only HTML files within a folder
```python
# import the glob module
import glob

# specify the file we desire to delete
fPath = r'C:\Users\Nagasudhir\Documents\Static_Web_Projects\WRLDC Apps Dashboard'

# use glob to get the filenames of html files in the folder using pattern matching
fNames = glob.glob(r'{0}\*.html'.format(fPath))

print(fNames)
'''
this will print
['C:\\Users\\Nagasudhir\\Documents\\Static_Web_Projects\\WRLDC Apps Dashboard\\cards.html', 
'C:\\Users\\Nagasudhir\\Documents\\Static_Web_Projects\\WRLDC Apps Dashboard\\index.html']
'''
```

### get all filenames including sub-folders files with 'recursive' option
As shown below, using `recursive = True` and in `\**\` the search pattern we can get filenames from sub-folders also
```python
# import the glob module
import glob

# specify the file we desire to delete
fPath = r'C:\Users\Nagasudhir\Documents\CSharp_Projects\EdnaMonitoring\src\EdnaMonitoring.App\Data'

# use glob to get the filenames of all .cs files in the folder using pattern matching
# notice that even sub-folders files are also included
fNames = glob.glob(r'{0}\**\*.cs'.format(fPath), recursive=True)

print(fNames)
'''
this will print
['C:\\Users\\Nagasudhir\\Documents\\CSharp_Projects\\EdnaMonitoring\\src\\EdnaMonitoring.App\\Data\\AppIdentityDbContext.cs', 
'C:\\Users\\Nagasudhir\\Documents\\CSharp_Projects\\EdnaMonitoring\\src\\EdnaMonitoring.App\\Data\\Configurations\\IctConfiguration.cs', 
'C:\\Users\\Nagasudhir\\Documents\\CSharp_Projects\\EdnaMonitoring\\src\\EdnaMonitoring.App\\Data\\Configurations\\MonitoringEntityConfiguration.cs', 
'C:\\Users\\Nagasudhir\\Documents\\CSharp_Projects\\EdnaMonitoring\\src\\EdnaMonitoring.App\\Data\\Configurations\\TransLineConfiguration.cs']
'''
```

### Example - get the size of each file in a folder using glob
```python
import glob
import os

folPath = r'C:\Users\Nagasudhir\Documents\Python Projects\ping_status_dump_creation'

for fPath in glob.glob("{0}\**\*.bat".format(folPath), recursive=True):

	# get file size

	fSize = os.stat(fPath).st_size/1024

	print('size of {0} is {1}'.format(fPath, fSize))
```

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* https://www.geeksforgeeks.org/how-to-use-glob-function-to-find-files-recursively-in-python/
* https://docs.python.org/3.8/library/glob.html
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEl0ZXJhdGUgdGhyb3VnaC
BmaWxlcyBpbnNpZGUgZm9sZGVyXG5hdXRob3I6IE5hZ2FzdWRo
aXIgUHVsbGFcbmRhdGU6ICcyMDIwLTA2LTAxJ1xudGFnczogJ2
xlYXJuaW5nLCBweXRob24sIHRhbWluZ19weXRob25fc2tpbGwn
XG5jYXRlZ29yaWVzOiB0YW1pbmdfcHl0aG9uX3NraWxsXG4iLC
JoaXN0b3J5IjpbLTE5NTkxNTU2MzYsLTMxMTk1NTAsNDQzMjM3
NTgzLDg1NzE5Njk1M119
-->