## Skill - Installing and using DBeaver for accessing and controlling different databases in one tool

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>
In this post we will try to install and use a free universal database tool called [DBeaver](https://dbeaver.io/).

![DBeaver_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/DBeaver_demo.png)

## Why use DBeaver
* You can manage all popular databases (MySQL, PostgreSQL, SQLite, Oracle, DB2, SQL Server, MS Access, Teradata, Firebird, Apache Hive, Phoenix, Presto, etc) in one single tool. No need to download separate tool for each type of database
* The community edition of DBeaver is free
* This is tool is cross-platform, so it can be installed in Windows, Linux, Mac

## Install DBeaver
#### Windows
* Download DBeaver at https://dbeaver.io/download/
* Run the installer and complete the installation

#### Ubuntu
```bash
sudo add-apt-repository ppa:serge-rider/dbeaver-ce
sudo apt-get update
sudo apt-get install dbeaver-ce
```
#### Other Linux Distributions
The DBeaver download page at https://dbeaver.io/download/ has the commands and instructions required to install in other environments also like Debian, Mac OS, RPM etc

### Using DBeaver
![dbeaver_new_connection_screen](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/dbeaver_new_connection_screen.png)
* Each type of database connection requires its own plugin
* If plugin is not present in the computer, DBeaver will prompt to install the plugins via downloading from the internet

## Installing DBeaver plugins without internet
* First install the required drivers in a PC with internet
* All the installed database plugins can be found in the folder
```C:\Users\<username>\AppData\Roaming\DBeaverData\drivers\maven\maven-central```
* On the Top Menu bar goto Database -> DriverManager menu
* Then select the database you would
### Video
The video for this post can be found [here](https://youtu.be/ErUPLbqXiB8)

### References
* DBeaver download - https://dbeaver.io/download/
* DBeaver site - https://dbeaver.io

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NzI0MjA3ODcsLTQ3Nzg0MTkwNiwtMT
c4MzczOTYwLC0xNDg5Njc1NzY3LDE4OTM0MzY1NzEsLTk5NTQ0
MzIxOSwtNjMwMDUyNjMxLDEzNDU0OTEzMV19
-->