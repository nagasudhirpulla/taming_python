## Skill - Installing PostgreSQL database
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>
In this post we will try to install a PostgreSQL database.

## Why is database needed
* Database is needed to persist data/state of an application in the storage for analytics, business logic implementation etc
* Database make some common tasks very easy and manageable like  data storage with encryption, querying the stored data, creating reports etc
* Almost all practical software systems will require a database to persist the data

Sometimes the computer in which the python code has to run 
* may not have python installed in it
* may not have  internet to install python
* may not have additional package dependencies
* may have conflicting versions of python libraries

All the above issues in python code deployment can be solved by distributing our python code along with python and its dependencies as an independent folder with `.exe` file to run the code.

This can be done using the `pyinstaller` package

To install it, run the command `pip install pyinstaller` in command prompt.

### Packaging our code with pyinstaller command
* Go to the folder in which our desired python script is located
* Right click and select 'open command window here'
* Here `index.py` is the python code entry point. Hence, in command prompt type `pyinstaller index.py` and press Enter.  
![pyinstaller_command](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/pyinstaller_command.png)
* pyinstaller now creates a packaged folder of our python script inside the `dist` folder. Since our python file is `index.py`, you should see a folder named `index` with a file `index.exe` inside it.
![pyinstaller_folders](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/pyinstaller_folders.png)
* Now the `index` folder can be deployed in any windows machine

### --onefile flag to create just a single exe file
running the command ```pyinstaller index.py --onefile``` will just create a single .exe file instead of a folder

One drawback of using pyinstaller is that all the packages and python itself is packaged inside the deployment folder. This increases the size of deployment.

### Video

You can the video on this post [here](https://youtu.be/kxGXvpg0Zno)

<iframe width="560" height="315" src="https://www.youtube.com/embed/kxGXvpg0Zno" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* Official docs - https://www.pyinstaller.org/
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg1MzU4NjIzOV19
-->