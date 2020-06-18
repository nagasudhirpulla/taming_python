## Skill - PyInstaller
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)


Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>
In this post, we will learn how to distribute our python program as `.exe` file

Sometimes the computer in which the python code has to run 
* may not have python installed in it
* may not have  internet to install python
* may not have additional package dependencies
* may have conflicting versions of python libraries

All the above issues in python code deployment can be solved by distributing our python code along with python and its dependencies as an independent folder with `.exe` file to run the code.

This can be done using the `pyinstaller` package

To install it, run the command `pip install pyinstaller` in command prompt.

### Packaging our code with pyinstaller command
* Go to the folder in which our python script is located
* Right click and select 'open command window here'
* In command prompt type `pyinstaller index.py`. Here `index.py` is the python code entry point. You can replace `index.py` with your filename
* pyinstaller now creates a packaged folder of the python script inside `dist` folder. Since our python file is `index.py`, you should see a folder named `index` with a file `index.exe` inside it.
* Now the `index` folder can be deployed in any windows machine

### References
* Official docs - https://www.pyinstaller.org/
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFVzaW5nIFB5SW5zdGFsbG
VyIGZvciBkaXN0cmlidXRpbmcgcHl0aG9uIHByb2dyYW1cbmF1
dGhvcjogTmFnYXN1ZGhpciBQdWxsYVxuZGF0ZTogJzIwMjAtMD
YtMTgnXG4iLCJoaXN0b3J5IjpbMTkyNDEwMTYzMF19
-->