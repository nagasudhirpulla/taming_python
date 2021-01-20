
## Skill - Managing application configuration and sensitive data using a JSON file
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [strings in python](https://nagasudhir.blogspot.com/2020/04/strings-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

It is not advisable to keep application configuration or sensitive data like usernames , passwords, api keys, port numbers in the source code or hard-code them in our code. The reasons not to do so is
* You have to change and re-deploy the code once the usernames, passwords change
* We can accidentally commit our code to open source repositories like GitHub etc., where our sensitive data will be exposed

One of the easy ways to maintain sensitive data is using `JSON file` as application configuration file. 
The advantages of storing application configuration in a JSON file is 
* Data is not hard-coded in the application code. Hence no need to change code when usernames, passwords, port numbers change
* If mentioned in .gitignore file, the config JSON file will not be pushed to source control like git

### Sample config.json file
```json
{
"username": "john",
"password": "superSecret",
"port": 80
}
```

### simple scenario with only one script file
```python
# import json module
import json
def loadAppConfig(fName="config.json"):
    with open(fName) as f:
        global appConf
        appConf = json.load(f)
        return appConf

# load config data from json file
# and store in a variable
appConf = loadAppConfig()

# use this appConf object in your script
print(appConf)
print('username is {0}'.format(appConf['username']))
print('password is {0}'.format(appConf['password']))
```

### caching config file data to prevent multiple JSON file reads
create a python file by name ```appConfig.py``` in the same folder as that of ```config.json```
```python
# appConfig.py

# import json module
import json

# initialize the app config global variable
appConf = {}

# load config json into the global variable
def loadAppConfig(fName="config.json"):
    with open(fName) as f:
        global appConf
        appConf = json.load(f)
        return appConf

# get the cached application config object
def getAppConfig():
    global appConf
    return appConf
```

### Using app config data in the script
```python
### index.py
# import the required functions from appConfig.py file
from appConfig import getAppConfig, loadAppConfig

# load app config data from json file
configDict = loadAppConfig()
print(configDict)

print("******************")

# using getAppConfig() to access config data
# after loading it once
print(getAppConfig())
```

### Video
The video tutorial for this post can be found [here](https://youtu.be/9cJN9D_OqTI)

<iframe width="560" height="315" src="https://www.youtube.com/embed/9cJN9D_OqTI" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/ , https://repl.it/

<hr/>

### References
* python json module official documentation - https://docs.python.org/3/library/json.html

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IE1hbmFnZSBhcHBsaWNhdG
lvbiBjb25maWd1cmF0aW9uIHdpdGgganNvbiBmaWxlXG5hdXRo
b3I6IE5hZ2FzdWRoaXIgUHVsbGFcbnRhZ3M6ICd0YW1pbmdfcH
l0aG9uLCB0YW1pbmdfcHl0aG9uX3NraWxsJ1xuY2F0ZWdvcmll
czogdGFtaW5nX3B5dGhvbl9za2lsbFxuZGF0ZTogJzIwMjEtMD
EtMjAnXG4iLCJoaXN0b3J5IjpbLTEwNDkyNDk2NDEsLTYxNzY1
ODc3OCwtMTc0ODEwOTg5OCwtMTYxNjg5Njc3OSwxOTAwMTM3MD
AyXX0=
-->