## Skill - Dictionaries in Python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

A Dictionary contains a set of key-value pairs encapsulated in it

### Main Code
#### Create a dictionary
```python
# create a dictionary
x = {'firstname': 'Nagasudhir', 'lastname': 'Pulla'}
```
### Access value using it's key
```python
# create a dictionary
xDict = {
    'firstName': 'Nagasudhir',
    'lastname': 'Pulla',
    'age': 28,
    'hobbies': ['tv', 'playing', 'youtube'],
    'location': 'Mumbai',
    'metaData': {
        'proficiency': 'level 1',
        'designation': 'Deputy Manager',
        'department': 'IT',
        'languages': ['C#', 'Javascript', 'HTML', 'CSS', 'typescript', 'python']
    }
}

# access firstName value
print(xDict['firstName'])
# prints Nagasudhir

# access lastname value
print(xDict['lastname'])
# prints Pulla

outputStatement = 'The person name is {0} {1}.\nHe lives at {2}, his hobbies are {3}.\nHe knows {4}'\
    .format(xDict['firstName'], xDict['lastname'], xDict['location'],
            ', '.join(xDict['hobbies']), ', '.join(xDict['metaData']['languages']))
print(outputStatement)
''' This should print
The person name is Nagasudhir Pulla.
He lives at Mumbai, his hobbies are tv, playing, youtube.
He knows C#, Javascript, HTML, CSS, typescript, python
'''
```

### Check if dictionary has a key using "in" operator
```python
# create a dictionary
x = {'firstname': 'Nagasudhir', 'lastname': 'Pulla'}

print('firstname' in x)
# prints True

print('somethingElse' in x)
# prints False
```

### List out all the keys and values of a dictionary
```python
# create a dictionary
x = {'firstname': 'Nagasudhir', 'lastname': 'Pulla'}

# print all the keys
print(list(x.keys()))
# prints ['firstname', 'lastname']

# print all the values
print(list(x.values()))
# prints ['Nagasudhir', 'Pulla']
```

### Create / Edit values in a dictionary
```python
# create a dictionary
x = {'firstname': 'Nagasudhir', 'lastname': 'Pulla'}

# change firstname
x['firstname'] = 'Sudhir'

# create a new property with key as 'age'
x['age'] = 28

# print the dictionary
print(x)
# prints {'firstname': 'Sudhir', 'lastname': 'Pulla', 'age': 28}
```

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/PaleTealFact?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IERpY3Rpb25hcmllcyBpbi
BQeXRob25cbmF1dGhvcjogTmFnYXN1ZGhpciBQdWxsYVxuZGF0
ZTogJzIwMjAtMDUtMDEnXG50YWdzOiAnbGVhcm5pbmcsIHB5dG
hvbiwgdGFtaW5nX3B5dGhvbl9za2lsbCdcbmNhdGVnb3JpZXM6
IHRhbWluZ19weXRob25fc2tpbGxcbiIsImhpc3RvcnkiOls1Mz
k4MTgwMjMsLTUzMTcwMTUyNSw2NjQxNTcxMTQsLTgxNzk2MjEw
MSwtMTQyNDM4MTk2NiwtNDU0MTA4ODM4LC0xMTcxMDM4MTkwXX
0=
-->