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

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg2NzIzNjg3MywxNzA1Mjg5NDU5LC0xNz
Y4MTc3NjA3XX0=
-->