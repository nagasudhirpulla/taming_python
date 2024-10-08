## Skill - Basic printing in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)

Please make sure to go through all the skills mentioned above to understand and execute the code mentioned below

#### Main Code
In order to print the _Hello world!_ string, use the [print()](http://docs.python.org/library/functions.html#print "(in Python v2.7)") function as follows
```python
print("Hello world!")
```

### 'end' input to suppress new line
use 'end' input to print function to suppress new line for each print function call
```python
# space printed at the end instead of new line
print('Hello', end=' ')
# space printed at the end instead of new line
print('World', end=' ')
print('!!!')
```

### colored printing using the 'colored' module
Use ```pip install colored``` in command prompt to install `colored` module
```python
# import fg, bg, attr sub modules from colored module
from colored import fg, bg, attr

# print Hello World !!! with red foreground and blue background
print ('{0}{1}Hello World !!!{2}'.format(fg('red'), bg('blue'), attr('reset')))

# print Hello World !!! with green color
print ('{0}Hello World !!!{1}'.format(fg('green'), attr('reset')))
```
For more information on colors in `colored` module click [here](https://pypi.org/project/colored/)

#### Run this in Visual Studio Code
* Create a folder in your PC
* Open this folder in Visual Studio Code using menu _File->Open Folder_
* Open _File Explorer_
* Create a python file by any name, say ```hello.py``` and write the following
```python
print("Hello world!")
```
* Run the code using menu _Run -> Run Without Debugging_
* You should see __Hello world!__ printed in the terminal

### Video
The video for this post can be seen [here](https://youtu.be/VJhA5mhM9dw)

<iframe width="560" height="315" src="https://www.youtube.com/embed/VJhA5mhM9dw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

### References
* Official documentation - https://docs.python.org/3/library/functions.html#print
* `colored` module - https://pypi.org/project/colored/
* Colored printing guide - https://www.geeksforgeeks.org/print-colors-python-terminal/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEJhc2ljIHByaW50aW5nIG
luIHB5dGhvblxuYXV0aG9yOiBOYWdhc3VkaGlyIFB1bGxhXG50
YWdzOiAncHl0aG9uLCBsZWFybmluZywgdHV0b3JpYWwnXG5jYX
RlZ29yaWVzOiB0YW1pbmdfcHl0aG9uX3NraWxsXG5kYXRlOiAn
MjAyMC0wNC0xNSdcbiIsImhpc3RvcnkiOls0MDQ5NzMyNjMsND
k4MjkxODI5LC0xODA5ODcyODY3LDg2MjQzMTMyMSwtMTA4OTk2
MzY4MiwxMzk3MDA1NTMyLC0xNjc0Mjg5MjUxLDE4MDQzNjkxNT
AsMzk2MjQxODUwLC0yMDcwMTQxMjgwLDQyMTYwNzk3NywtMTI2
MzI0NTU4MCwxMzU5MjQyOTYyLDc3NjczMzI4NF19
-->