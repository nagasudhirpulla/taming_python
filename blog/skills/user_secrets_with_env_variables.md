## Skill - Accessing application secrets with environment variables
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [strings in python](https://nagasudhir.blogspot.com/2020/04/strings-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

It is not advisable to keep sensitive application data like usernames , passwords, api keys in the source code or hard-code them in our code. The reasons not to do so is
* You have to change and re-deploy the code once the usernames, passwords change
* We can accidentally commit our code to open source repositories like GitHub etc., where our sensitive data will be exposed

One of the easy ways to maintain sensitive data is using `system environment` variables. 
The advantages of storing sensitive application data in system environment variables is 
* Data is not hard-coded in the application code. Hence no need to change code when usernames, passwords change
* Environment variables are not present in the application code folder. Hence sensitive data will not be pushed to source control like git and sensitive data cannot be taken just by copy pasting the application code folder.
* Environment variables can be edited only if a person enters the credentials of the machine/computer.

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
### Video
The video tutorial for this post can be found [here](https://youtu.be/9cJN9D_OqTI)

<iframe width="560" height="315" src="https://www.youtube.com/embed/IZBrA4Sn40k" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/ , https://repl.it/

<hr/>

### References
* https://www.geeksforgeeks.org/python-os-getenv-method/
* https://docs.python.org/3/library/os.html#os.getenv
* https://stackoverflow.com/questions/16924471/difference-between-os-getenv-and-os-environ-get

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEFjY2Vzc2luZyBhcHBsaW
NhdGlvbiBzZWNyZXRzIHdpdGggZW52aXJvbm1lbnQgdmFyaWFi
bGVzXG5hdXRob3I6IE5hZ2FzdWRoaXIgUHVsbGFcbnRhZ3M6IC
dsZWFybmluZywgcHl0aG9uLCB0YW1pbmdfcHl0aG9uX3NraWxs
J1xuY2F0ZWdvcmllczogdGFtaW5nX3B5dGhvbl9za2lsbFxuZG
F0ZTogJzIwMjAtMDYtMzAnXG4iLCJoaXN0b3J5IjpbLTU2NjE1
NjU4MCwxNzMxOTE4MjkxLDE2MDI2NzUwOTEsMjA4ODI3ODM3My
wtMzQ2NzA4OTE5LC0xMjEwMjY2NzQsLTExOTY1Nzk4ODAsLTk1
OTg4NjM1OSwyMDUzNjkwNDI5XX0=
-->