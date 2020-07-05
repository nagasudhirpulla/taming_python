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

### File paths in the 'from' statement while importing
* In `get_all_persons_Info.py` file statement used to import the function `createInfoForPerson` was
``` python
from utils.info_creator import createInfoForPerson
```
* Even though `info_creator.py` file is in the same folder as that of `get_all_persons_Info.py`, we used `utils.info_creator`
* this is because, the file-path during import should be based on the entry python file. In our case the entry file was `index.py` and hence the import path is with respect to `index.py` as `utils.info_creator`

### Executing the example application code
* The code should be executed by running `index.py`
* If we run other files in the folders, we will get errors at the import statements because the imports are all defined at the folder level of `index.py`
* Hence all the code that is to be executed needs to be in the same folder as that of entry file (`index.py`) in order to avoid import errors. This is a constraint to be considered in the application code design in order to use shared variables and functions concept.

### Points to remember
* file-paths used in the import statements are to be written relative to the entry python file, not as per the python file in which the import statement.
Many people get confused with this concept
* ensure `__init__.py` file is in all folders in which the variables of python files are to be shared

<hr/>

### References
* https://codeburst.io/importing-variables-from-other-files-in-python-96a200f410da
* https://en.wikibooks.org/wiki/A_Beginner%27s_Python_Tutorial/Importing_Modules

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFNoYXJpbmcgZnVuY3Rpb2
5zIGFuZCB2YXJpYWJsZXMgYWNyb3NzIGZpbGVzIGluIHB5dGhv
blxuYXV0aG9yOiBOYWdhc3VkaGlyIFB1bGxhXG5kYXRlOiAnMj
AyMC0wNy0wNSdcbnRhZ3M6ICdsZWFybmluZywgcHl0aG9uLCB0
YW1pbmdfcHl0aG9uX3NraWxsJ1xuY2F0ZWdvcmllczogdGFtaW
5nX3B5dGhvbl9za2lsbFxuIiwiaGlzdG9yeSI6Wy0zOTAzOTEw
NDUsLTE5NjM4NzI2MywxOTYyNTM1MjE2LDEwMTQ4NDE5NDddfQ
==
-->