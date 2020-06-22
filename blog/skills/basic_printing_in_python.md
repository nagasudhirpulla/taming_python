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
# 
print ('{0}{1} Hello World !!! {2}'.format(fg('white'), bg('yellow'), attr('reset')))
```

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

```SKILL ID = SBASF```


### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/SeriousBriefFrontend?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### References
* Official documentation - https://docs.python.org/3/library/functions.html#print
* Colored printing guide - https://www.geeksforgeeks.org/print-colors-python-terminal/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEJhc2ljIHByaW50aW5nIG
luIHB5dGhvblxuYXV0aG9yOiBOYWdhc3VkaGlyIFB1bGxhXG50
YWdzOiAncHl0aG9uLCBsZWFybmluZywgdHV0b3JpYWwnXG5jYX
RlZ29yaWVzOiB0YW1pbmdfcHl0aG9uX3NraWxsXG5kYXRlOiAn
MjAyMC0wNC0xNSdcbiIsImhpc3RvcnkiOlsxMDg2NzE0NDI0LC
0xNjc0Mjg5MjUxLDE4MDQzNjkxNTAsMzk2MjQxODUwLC0yMDcw
MTQxMjgwLDQyMTYwNzk3NywtMTI2MzI0NTU4MCwxMzU5MjQyOT
YyLDc3NjczMzI4NF19
-->