## Skill - Reading and writing files in python
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

In this post, we will learn to read and write files in python

### Open a file using 'open' function
Opening a file is required for reading or writing to a file
```python
with open("test.txt",'w',encoding = 'utf-8') as f:
   # perform operations on the file
```
In the above example we use the filename input of `open` function as 'test.txt', means that the file should be in the same folder of python script file

We can also give **absolute file path**s like the example below
```python
with open(r"C:\Users\Nagasudhir\Documents\test.txt") as t:
```
### file mode in 'open' function
By default, the `open` function opens the file only for reading, i.e., read mode.
The mode of file opening can be specified using the `mode` input of the function. The main file open `mode` options are as shown below

-   '**r**' , for reading.
-   '**w**' , for writing (clears any previous file data).
-   '**a**' , for appending (adding new data at the end of file).
-   '**r+**' , for both reading and writing while preserving the old data
-   '**w+**' , for both reading and writing while erasing the old data

### writing to file using 'w' file mode
```python
# open the file in write mode using mode='w'
with open(r"C:\Users\Nagasudhir\Documents\test.txt", mode='w') as f:   
   f.write("The first line\n")
   f.write("This is the second line\nThis the third line")
```
The `\n` character will create a new line in the file as shown above.
It is also worth noting that `mode='w'` or `mode = 'w+'` will create the file if it does not exist.

### read the whole file content using 'read' function
```python
# open the file for reading
with open(r"C:\Users\Nagasudhir\Documents\test.txt", mode='r') as f:
   # read all the file content   
   fStr = f.read()
   # please note that once again calling f.read() will return empty string
   
   print(fStr)
   # this will print the whole file contents
```

### read each line file content using a for loop
```python
# open the file for reading
with open(r"C:\Users\Nagasudhir\Documents\test.txt", mode='r') as f:
   for ln in f:
      print(ln, end='')
      # this the line, end='' will avoid extra line in console
```

### load all the lines of a file into an array using 'readlines' function
```python
with open(r"C:\Users\Nagasudhir\Documents\test.txt", mode='r') as f:
   # load all the lines of the file into an array
   textLines = f.readlines()
   
   print(textLines)
   # this will print 
   # ['The first line\n', 'This is the second line\n', 'This the third line']
```

### Video
The video for this post can be seen [here](https://youtu.be/s3KUZBK1gSI)

<iframe width="560" height="315" src="https://www.youtube.com/embed/s3KUZBK1gSI" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* https://www.programiz.com/python-programming/file-operation
* Official docs on `open` function - https://docs.python.org/3/library/functions.html#open
* https://www.geeksforgeeks.org/file-handling-python/
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFJlYWRpbmcgYW5kIHdyaX
RpbmcgZmlsZXMgaW4gcHl0aG9uXG5hdXRob3I6IE5hZ2FzdWRo
aXIgUHVsbGFcbmRhdGU6ICcyMDIwLTA1LTMxJ1xudGFnczogJ2
xlYXJuaW5nLCBweXRob24sIHRhbWluZ19weXRob25fc2tpbGwn
XG5jYXRlZ29yaWVzOiB0YW1pbmdfcHl0aG9uX3NraWxsXG4iLC
JoaXN0b3J5IjpbNTMzMzk2Njc3LDE1MDQ5ODY3NzAsODkzMzcz
ODAxLDE2MjM2MjAwODAsLTE2MzA2NjYxNzVdfQ==
-->