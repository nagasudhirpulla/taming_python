## Skill - Creating a folder in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [strings in python](https://nagasudhir.blogspot.com/2020/04/strings-in-python.html)
* [raw strings in python](https://nagasudhir.blogspot.com/2020/05/raw-strings-in-python.html)
* [Handling errors in python](https://nagasudhir.blogspot.com/2020/05/hnadling-errors-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post, we will learn to create a folder using `mkdir` and `makedirs` function

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
We used try except to catch exception which can occur if the folder we are trying to create already exists

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

### Video
The video for this post can be seen [here](https://youtu.be/g3LJeQxpDao)

<iframe width="560" height="315" src="https://www.youtube.com/embed/g3LJeQxpDao" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* https://www.geeksforgeeks.org/create-a-directory-in-python/#makedirs
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IENyZWF0aW5nIGEgZm9sZG
VyIGluIHB5dGhvblxuYXV0aG9yOiBOYWdhc3VkaGlyIFB1bGxh
XG5kYXRlOiAnMjAyMC0wNS0zMSdcbnRhZ3M6ICdsZWFybmluZy
wgcHl0aG9uLCB0YW1pbmdfcHl0aG9uX3NraWxsJ1xuY2F0ZWdv
cmllczogdGFtaW5nX3B5dGhvbl9za2lsbFxuIiwiaGlzdG9yeS
I6Wy0zOTMwMjgxMTMsLTE3NjM4MTE1NTYsLTIwNjA0NTkwMTQs
MTE1Njc5ODYxNCwxNjI3MDYyMTg0XX0=
-->