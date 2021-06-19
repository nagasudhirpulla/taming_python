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

You can download the project files [here](https://github.com/nagasudhirpulla/sample_python_script_template/archive/refs/heads/main.zip)

![sample_python_project_virtual_env_folder](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/sample_python_project_virtual_env_folder.PNG)

### Scenario - Create a virtual environment from existing requirements.txt
Run / Double click the following batch files in the below sequence
* create_env.bat
* install_env.bat

### Scenario - Update the current virtual environment packages in requirements.txt
Run / Double click the following batch file
* freeze_env.bat

### Scenario - Run the python project with the created virtual environment
Run / Double click the following batch file
* run.bat
 
### Each batch file explained
* create_env.bat - creates a new virtual environment
* install_env.bat - installs packages from ```requirements.txt``` in the virtual environment
* activate_env.bat - activates the created virtual environment
* freeze_env.bat - writes all the virtual environment packages into ```requirements.txt``` file 
 
<hr/>

### Further Reading
* https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/#creating-a-virtual-environment

### Video

You can the video on this post [here](https://youtu.be/1FA83Ut5LL0)

<iframe width="560" height="315" src="https://www.youtube.com/embed/1FA83Ut5LL0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MDc2NzU5ODIsMTY0NDcyNDU2MiwxOD
Y3MjM2ODczLDE3MDUyODk0NTksLTE3NjgxNzc2MDddfQ==
-->