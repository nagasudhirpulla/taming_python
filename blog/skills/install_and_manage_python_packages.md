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
* Open command prompt inside that folder using Shift + right click
* Enter command `.\activate.bat`

### De-activate a virtual environment
* Goto 'Scripts' folder of the created virtual environment
* Open command prompt inside that folder using Shift + right click
* Enter command `.\deactivate.bat`

### Using a virtual environment in Visual Studio Code
In order to use a virtual environment in Visual Studio Code, follow the below steps
* Press *Ctrl+Shift+P*, select *Open Workspace Settings* as shown below.
![vs_code_open_workspace_settings](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/vs_code_open_workspace_settings.png)
* Click open settings button (page like icon on the top right). 
![vs_code_open_settings_json](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/vs_code_open_settings_json.png)
* This opens the .vscode > settings.json file as shown below. Then create a key value pair `"python.pythonPath" : "path\\to\\env_folder\\Scripts\\python.exe"` in *settings.json* file as shown below.
![vs_code_python_path_in_settings_json](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/vs_code_python_path_in_settings_json.png)
* This will make VS Code to use the created virtual environment.
* You can verify this by keeping your mouse at the bottom-left as shown below.
![vs_code_active_python_env_check](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/vs_code_active_python_env_check.png)
### Further Reading
* https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/#creating-a-virtual-environment

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEluc3RhbGwgYW5kIG1hbm
FnZSBwYWNrYWdlcyBpbiBweXRob25cbmF1dGhvcjogTmFnYXN1
ZGhpciBQdWxsYVxuZGF0ZTogJzIwMjAtMDUtMjUnXG50YWdzOi
AncHl0aG9uLCBsZWFybmluZywgdHV0b3JpYWwsIHRhbWluZ19w
eXRob25fc2tpbGwnXG5jYXRlZ29yaWVzOiB0YW1pbmdfcHl0aG
9uX3NraWxsXG4iLCJoaXN0b3J5IjpbLTQzODc4NTMxNiwtMzg4
NTU4NDMwLDE1Nzk2NTQ0MTQsNTk1NjU3NDI2LDE2NDY1ODc4NC
wxMDk2Njk5MTU3LDE5MjU3ODQ5MTUsNzI2Njc0NTY4LDE0MTI3
NjAwNTQsMjEwMzkwMjQxLDczMDk5ODExNl19
-->