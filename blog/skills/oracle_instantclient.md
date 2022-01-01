## Skill - Oracle Instant Client installation in windows

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>
In this post we will install Oracle Instant Client that enables communication between python scripts and Oracle database.

## Why use Oracle Instant Client
* Without Oracle Instant Client, python scripts cannot communicate with the oracle database.

## When is Instant Client not required
* If you computer that is running the python scripts already has Oracle database installed in it, Instant Client may not be required.
* But there can be cases where the Oracle is 32 bit and python is 64 bit or vice-versa, where Instant Client installation will be necessary even if Oracle Database is installed in the computer.

## Downloading the Instant Client
* Download Oracle Instant Client from https://www.oracle.com/database/technologies/instant-client/downloads.html or search for "Oracle Instant Client download" if this link does not work
* Download the relevant zip file by clicking on the link like "Instant Client for Microsoft Windows (x64)"
* Download the basic package zip file

## Installing Instant Client in Windows machine
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



### References
* Oracle Instant Client documentation - https://www.oracle.com/in/database/technologies/instant-client.html
* Cx_Oracle documentation - https://oracle.github.io/python-cx_Oracle/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU1OTIxNjEwOV19
-->