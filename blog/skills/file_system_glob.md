## Skill - iterate through files in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

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

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* https://thispointer.com/python-how-to-remove-a-file-if-exists-and-handle-errors-os-remove-os-ulink/
* https://stackoverflow.com/questions/6996603/how-to-delete-a-file-or-folder
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbOTQxNDM4MTAyLDg1NzE5Njk1M119
-->