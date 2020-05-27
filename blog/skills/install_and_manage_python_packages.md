## Skill - Install and manage python packages
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Install and manage python packages](https://nagasudhir.blogspot.com/2020/05/install-and-manage-packages-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

### Why virtual environments
* Each installed python package has a particular version number.
* Sometimes we may desire to have different version numbers of the same package for different python projects (may be due to compatibility issues).
* This can be solved by creating a virtual environment and using it in our project

### Introduction
* A virtual environment has its own python packages isolated from the default system python environment and its installed packages
* This way we can manage the packages installed and their version numbers and use it in our projects

### Create a virtual environment using 'venv'
* Create a folder
* Open command prompt inside that folder
* Enter command `python venv -m env_name` 
you can use any name instead of `env_name` 

### Activate a virtual environment
* Goto 'Scripts' folder of the created virtual environment
* Open command prompt inside that folder
* Enter command `.\activate.bat`

### De-activate a virtual environment
* Goto 'Scripts' folder of the created virtual environment
* Open command prompt inside that folder
* Enter command `.\deactivate.bat`

### Using a virtual environment in Visual Studio Code
In order to use a virtual environment in Visual Studio Code, follow the below steps
* Press Ctrl+Shift+P, open workspace settings and click open settings button (page like icon on the top right) to open the .vscode > settings.json file

### Further Reading
* https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/#creating-a-virtual-environment
* Then create a key value pair `"python.pythonPath" : "path\\to\\env_folder\\Scripts\\python.exe"`
* This will make VS Code to use the created virtual environment

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEluc3RhbGwgYW5kIG1hbm
FnZSBwYWNrYWdlcyBpbiBweXRob25cbmF1dGhvcjogTmFnYXN1
ZGhpciBQdWxsYVxuZGF0ZTogJzIwMjAtMDUtMjUnXG50YWdzOi
AncHl0aG9uLCBsZWFybmluZywgdHV0b3JpYWwsIHRhbWluZ19w
eXRob25fc2tpbGwnXG5jYXRlZ29yaWVzOiB0YW1pbmdfcHl0aG
9uX3NraWxsXG4iLCJoaXN0b3J5IjpbMTQ4NTM0MzA4LDU5NTY1
NzQyNiwxNjQ2NTg3ODQsMTA5NjY5OTE1NywxOTI1Nzg0OTE1LD
cyNjY3NDU2OCwxNDEyNzYwMDU0LDIxMDM5MDI0MSw3MzA5OTgx
MTZdfQ==
-->