## Skill - Oracle Express Edition (XE) database installation in Windows

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
* Download Oracle Instant Client Package - zip file
* Create an installation directory like ```C:\instantclient```
* Copy the zip file to the installation directory and unzip the zip file there. 
* Now all the instant client files will be in the folder ```C:\instantclient```
* Include the above folder path ```C:\instantclient\``` in ```PATH``` and ```OCI_LIB64``` system environment variables
* If we get an error in python script something like "32 bit instant client not found", then remove the 64 bit files and folders and install a 32 bit version of Instant Client.

## Interfacing with Oracle database in python scripts
* Along with Oracle Instant client, we also need ```cx_Oracle``` python module to interface with Oracle database in python scripts
* To install cx_Oracle python module, run the following command in the python environment
```
python -m pip install cx_Oracle
```

### Video
You can the video on this post [here](https://youtu.be/v0TkfVFGO5c)

<iframe width="560" height="315" src="https://www.youtube.com/embed/v0TkfVFGO5c" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


### References
* Oracle Instant Client documentation - https://www.oracle.com/in/database/technologies/instant-client.html
* cx_Oracle home page - https://oracle.github.io/python-cx_Oracle/
* cx_Oracle documentation - https://cx-oracle.readthedocs.io/en/latest/user_guide/installation.html#quick-start-cx-oracle-installation

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUxNzE5NzM4MywtMzc5OTI0OTZdfQ==
-->