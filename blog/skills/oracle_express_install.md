## Skill - Oracle Express Edition (XE) database installation in Windows and connect with DBeaver

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
* Download Oracle database zip file
* If the `ORACLE_HOME` environment variable has been set, then use System in the Control Panel to delete it.
* Unzip the files
* Run the setup.exe to install the database

## Using DBeaver to connect to the Oracle database
* 


### References
* Oracle Instant Client documentation - https://www.oracle.com/in/database/technologies/instant-client.html
* cx_Oracle home page - https://oracle.github.io/python-cx_Oracle/
* cx_Oracle documentation - https://cx-oracle.readthedocs.io/en/latest/user_guide/installation.html#quick-start-cx-oracle-installation

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbNjI5MTU3MTgxLC01MTcxOTczODMsLTM3OT
kyNDk2XX0=
-->