## Skill - Installing PostgreSQL database
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>
In this post we will try to install a PostgreSQL database.

## Why is a database required
* Database is needed to persist data/state of an application in the storage for analytics, business logic implementation etc
* Database makes some common tasks very easy and manageable like  data storage with encryption, querying the stored data, creating reports etc
* Almost all practical software systems will require a database to persist the data

## What is a PostgreSQL database
* PostgreSQL database is a powerful opensource relational database where data can be stored in tables
* We can achieve very robust data integrity with foreign keys, primary keys, uniqueness constraints, data types, enforcing data size limitations / value ranges, triggers etc

## Installing PostgreSQL database
### Windows
* Download the installer from https://www.postgresql.org/download/windows/
* run the download installer and install the software
### Linux based systems
* PostgreSQL is already shipped with many linux distributions like Ubuntu. 
* To check the version of PostgreSQL, run the ```postgres -V``` command
* If you want to install specific versions, the commands for installing are provided in the official postgres website at https://www.postgresql.org/download/
#### Ubuntu installation commands
```bash
# Create the file repository configuration:
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'

# Import the repository signing key:
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

# Update the package lists:
sudo apt-get update

# Install the latest version of PostgreSQL.
# If you want a specific version, use 'postgresql-12' or similar instead of 'postgresql':
sudo apt-get -y install postgresql
```



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
eyJoaXN0b3J5IjpbMTM1NDk4NTUzMyw5NjI5MjcwNzQsLTY0MD
ExMzczNSwtODUzNTg2MjM5XX0=
-->