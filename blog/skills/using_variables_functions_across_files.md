## Skill - Sharing functions and variables across files in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

Sharing variables and functions defined in one file with other files can be very useful to
* reduce the size and duplication of the application code by defining variables and function only in one file
* increase the readability and maintainability of the application code, since we can split the code across different files and folders
* implement coding practices like separation of concerns, single responsibility principle etc.,

<hr/>

### Folder structure for this example
![sharing_variables_demo_file_structure](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/sharing_variables_demo_file_structure.png)
* Entry file for executing this application is `index.py`
* The code of our example python application will be distributed across the folders as shown in the above image
* Notice that each folder has `__init__.py` file inside it. This is required for sharing the code inside the folder.
Hence ensure each folder has `__init__.py` file inside it

### Code in each file
```python
# stores/persons_store.py
persons = [
    {'name': 'Sudhir', 'age': '28'},
    {'name': 'Lakshmi', 'age': '27'},
    {'name': 'Aditya', 'age': '27'},
    {'name': 'Kishore', 'age': '24'},
]
```
<hr/>

```python
# utils/info_creator.py
def createInfoForPerson(p):
    return 'Name - {0}, Age - {1}'.format(p['name'], p['age'])
```
<hr/>

```python
# utils/get_all_persons_Info.py
from stores.persons_store import persons
from utils.info_creator import createInfoForPerson

def getAllPersonsInfo():
    infoArray = []
    for p in persons:
        personInfo = createInfoForPerson(p)
        infoArray.append(personInfo)
    return infoArray
```
<hr/>

```python
# index.py
from utils.get_all_persons_Info import getAllPersonsInfo

personsInfoList = getAllPersonsInfo()

print('All persons in the store are ...')
print('\n'.join(personsInfoList))
```
<hr/>


### Points to remember
* file-paths used in the import statements are to be written as per the entry python file, not as per the python file in which the import statement.
Many people get confused with this concept
* ensure `__init__.py` file is in all folders in which the variables of python files are to be shared

### Creating environment variables in a windows machine
* Open 'Edit system environment variables' from windows search bar 

![edit_sys_env_variables_in_start_menu](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/edit_sys_env_variables_in_start_menu.png)
* Click on 'Environment Variables' button
* Click on 'New' button in 'System Variables' section
* Enter environment variable name and value and click ''OK'

![creating_system_env_variable](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/creating_system_env_variable.png)
You can also edit or delete a system environment variable in the same manner

In our example shown in the figure, we created an environment variable named `app_password` and its value is `mysupersecret`

### accessing system environment variables using 'os.getenv' function
```python
# import os module
import os

# access the environment variable named 'app_password'
# The value returned when environment variable is not present in the stystem is given as the second input
val = os.getenv('app_password', 'default_value')

print('The value of app_password is {0}'.format(val))
# this should print
# The value of app_password is mysupersecret
```
![env_var_output](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/env_var_output.png)
### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/ , https://repl.it/

<hr/>

### References
* https://www.geeksforgeeks.org/python-os-getenv-method/
* https://docs.python.org/3/library/os.html#os.getenv
* https://stackoverflow.com/questions/16924471/difference-between-os-getenv-and-os-environ-get

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA4ODIwMDEyMiwxMDE0ODQxOTQ3XX0=
-->