## Skill - Using virtual environments in python projects

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Install and manage python packages](https://nagasudhir.blogspot.com/2020/05/install-and-manage-packages-in-python.html)
* [Virtual environments using 'venv'](https://nagasudhir.blogspot.com/2020/05/virtual-environments-using-venv.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

### Demo Project with virtual environment
A sample python demo project with virtual environment is hosted at https://github.com/nagasudhirpulla/sample_python_script_template

You can download the project files [here](https://github.com/nagasudhirpulla/sample_python_script_template.git)



### Introduction
* A virtual environment has its own python packages isolated from the default system python environment and its installed packages
* This way we can manage the packages installed and their version numbers and use it in our projects

### Create a virtual environment using 'venv'
* Create a folder
* Open command prompt inside that folder
* Enter command `python -m venv env_name` 
you can use any name instead of `env_name` 

### Activate a virtual environment
* Open a command prompt inside the project folder using Shift + right click
* If the virtual environment name is ```project_env```, Enter command `project_env\Scripts\activate.bat`

### Managing packages inside a virtual environment
* Once the virtual environment is activated, you can manage the environment packages as usual using `pip`. For more information, go through [this post](https://nagasudhir.blogspot.com/2020/05/install-and-manage-packages-in-python.html) on managing python packages

### Leaving a virtual environment
* Open a command prompt inside the project folder using Shift + right click
* If the virtual environment name is ```project_env```, Enter command `project_env\Scripts\deactivate.bat`

### Using a created virtual environment in Visual Studio Code
In order to use a created virtual environment in Visual Studio Code, follow these steps.
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

### Video

You can the video on this post [here](https://youtu.be/Gp7Eb4D1qnI)

<iframe width="560" height="315" src="https://www.youtube.com/embed/Gp7Eb4D1qnI" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM4NzEzOTc5Nl19
-->