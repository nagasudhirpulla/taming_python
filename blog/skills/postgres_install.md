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
## pgAdmin for database administration
* The PostgreSQL database administration can be very easily done using the  pgAdmin opensource tool
* It is included with most of the postgreSQL database installations
* You can easily create/view/update/delete the databases, tables, columns, rows, data, import/export data, run queries etc. using this tool
* Also it facilitates observability for the database sessions, I/O, transactions, statistics etc via a dashboard screen
![pgAdmin_snap](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/pgAdmin_snap.png)
## Access postgreSQL database remotely using the DBeaver tool
![DBeaver_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/DBeaver_demo.png)
* DBeaver is also a tool like pgAdmin to access postgreSQL or many other types of databases
* 

### References
* Official docs - https://www.postgresql.org/docs/14/index.html
* 
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MDI0Nzk4OTgsMTk4NTg4OTg5OCwtMT
U5OTk1NzM4NCwtMTQxODg2ODUzNiwtOTE1MTIxMDEyLDEzNTQ5
ODU1MzMsOTYyOTI3MDc0LC02NDAxMTM3MzUsLTg1MzU4NjIzOV
19
-->