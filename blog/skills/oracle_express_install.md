## Skill - Oracle Express Edition (XE) database setup along with sqldeveloper and DBeaver in Windows

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<hr/>
In this post we will install Oracle Express Edition (XE) database which is free and is meant for local and light weight database setup.

Oracle Express database is ideal for local development and testing without connecting to remote databases

## Limitations in Oracle express edition
Since Oracle Express database is free, there are some limitations
* Only one CPU will be used even if the computer has multiple cores and CPUs
* Maximum of 11 GB data storage is only supported, if you try to store more than that, the database will throw `ORA-12592` error
* Not more than 1 GB RAM will be used by the database
* HTTPS is not supported

In a nutshell, don't use it for production, use it only for testing and development purposes.

Detailed information about the limitations of Oracle Express database can be seen [here](https://docs.oracle.com/cd/E17781_01/install.112/e18803/toc.htm#XEINW117)

## Download Oracle Express Edition (XE) database
* Download Oracle Express Edition (XE) database from https://www.oracle.com/in/database/technologies/xe-downloads.html or search for "download oracle express edition" if this link does not work
* Download the relevant zip file by clicking on the link like " Oracle Database 21c Express Edition for Windows x64"

## Installing Oracle Express Edition in Windows
* If the `ORACLE_HOME` environment variable has been set, delete it.
* Download Oracle database zip file
* Unzip the files
* Run the setup.exe to install the database
* During the setup set the database password
 The official setup guide can be found [here](https://docs.oracle.com/cd/E17781_01/install.112/e18803/toc.htm#XEINW123)

## Start or Stop the Oracle database
* run ```services.msc``` command to open the services window
* Right click on the ```OracleServiceXE``` service and select stop or start to start or stop the oracle database

## Disable Automatic Startup of Oracle database upon system start
* run ```services.msc``` command to open the services window
* Right click on the ```OracleServiceXE``` service and select properties. Then select Startup type to "Manual" if you want the database to not start automatically on system start.

## Connecting to Oracle database with sqldeveloper
* sqldeveloper is the database administration client tool by Oracle.
* Download the tool from [here](https://www.oracle.com/tools/downloads/sqldev-downloads.html)
* 

## Connecting to Oracle database with DBeaver 
* DBeaver community edition is a free universal database management tool that supports many databases including Oracle
* Download DBeaver from [here](https://dbeaver.io/download)
* Check my post on DBeaver setup [here](https://nagasudhir.blogspot.com/2021/12/installing-and-using-dbeaver-for.html)
* For connecting to Oracle database, click new connection button at the top-left, select the database as Oracle and fill up the connection settings as shown in the image below.
![oracle_conn_setup_dbeaver](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/oracle_conn_setup_dbeaver.PNG)* You can click the "Test Connection" button to check if the settings are correct. Finally click the "Finish" button.

### Video
You can the video on this post [here](https://youtu.be/89h-pfIpNL8)

<iframe width="560" height="315" src="https://www.youtube.com/embed/89h-pfIpNL8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* Oracle Express (XE) database installation guide - https://docs.oracle.com/cd/E17781_01/install.112/e18803/toc.htm#XEINW123
* Oracle Express (XE) database download - https://www.oracle.com/in/database/technologies/xe-downloads.html
* Oracle Express (XE) database limitations - https://docs.oracle.com/cd/E17781_01/install.112/e18803/toc.htm#XEINW117

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNTQyNDYzMTQsLTU4NDE2OTAxNiwtMT
A5ODA5NjI3NiwtMTQ4MjIxOTAwMCwtMTM2NDY0NzUxOCwtMjAw
Mzg2NTE1MSwtNTE3MTk3MzgzLC0zNzk5MjQ5Nl19
-->