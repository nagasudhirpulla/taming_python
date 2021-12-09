## Skill - Using psycopg2 python module for PostgreSQL interfacing
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>
In this post we will use psycopg2 python module for interfacing with PostgreSQL database.

## Why is a database required
* Database is useful to persist the data/state of an application in the storage for analytics, business logic implementation etc
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
* If you manage multiple types of databases you can use DBeaver for managing all databases in one software

### Video
The video for this post can be found [here](https://youtu.be/ErUPLbqXiB8)

<iframe width="560" height="315" src="https://www.youtube.com/embed/ErUPLbqXiB8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* psycopg2 documentation - https://www.psycopg.org/docs/usage.html
* PostgreSQL Official docs - https://www.postgresql.org/docs/14/index.html
* pgAdmin download - https://www.pgadmin.org/download/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI3MzUwMDIxNCwtMTE1MzY3MTU4Ml19
-->