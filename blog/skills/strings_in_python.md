## Skill - Strings in Python

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

**string** means a group of characters

### Main Code
#### Creating a string
```python
x = 'This is string'
y = "You can use single or double quotes"
z = '''You can write multi-line strings using triple quotes
like this
Isn't that handy
'''
```

### Substituting variables in string using formatter
```python
someStr = 'Greetings from {0}, welcome to {1}'.format('sudhir', 'taming python')
# this will print 
# Greetings from sudhir, welcome to taming python

# notice how we substituted variables using {0}, {1}
# This way we can easily embed variables in strings
```

### Another way of substituting variables in string using formatter
```python
someStr = 'Greetings from {nameStr}, welcome to {courseStr}'.format(nameStr='sudhir', courseStr='taming python')
# this will print 
# Greetings from sudhir, welcome to taming python

# notice how we substituted named variables
# This way we can easily embed variables in strings
```

### title(), capitalize(), lower(), upper() and swapcase() functions
```python
# lower() will make all characters of string as lower case
print(x.lower())
# this will print 
# hello my dear friends!!!

# upper() will make all characters of string as upper case
print(x.upper())
# this will print 
# HELLO MY DEAR FRIENDS!!!

# title() will capatalize each word
x = 'hello my dear Friends!!!'
print(x.title())
# this will print 
# Hello My Dear Friends!!!

# capitalize() will capatalize only first letter of string
print(x.capitalize())
# this will print 
# Hello my dear friends!!!

# swapcase() will reverse the case of all the characters of a string
print(x.swapcase())
# this will print 
# HELLO MY DEAR fRIENDS!!!
```

### strip() function to remove spaces at beginning and end
```python
x = "  string with left and right spaces   "
print(mystr.strip())
# string with left and right spaces

x = "string with right spaces   "
print(mystr.strip())
# string with right spaces

x = "  string with left spaces"
print(mystr.strip())
# string with left spaces
```

### replace() function
````python
x = 'this is normal string, just a normal one'
y = x.replace('normal', 'great')
print(y)
# this is great string, just a great one

y = x.replace('normal', 'great', 1)
# only first occurence will be replaced, notice the third input of the function
# this is great string, just a normal one
```

### split() function
````python
# this is create a list of strings based on the specified seperator
x = 'one,two,three,four'
y = x.split(',')
print(y)
# ['one','two','three','four']

### join() function
y = message = ' '.join(['this' ,'is', 'a', 'useful', 'method'])
# only first occurence will be replaced, notice the third input of the function
# this is great string, just a normal one
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3MzIyNzY5NzQsMTI2NDQ4MDg4MiwxND
Y5OTgwMjQxLC00MTI0MjAwMjYsMTE4MzI5MTMyMV19
-->