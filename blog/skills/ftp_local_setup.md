## Skill - Setup ftp server and client in Windows using IIS, Filezilla server and WinSCP

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>

In this post we will try to setup a local ftp server using IIS or Filezilla server and ftp client using WinSCP

## Setup FTP server using IIS in windows server
### Enable IIS ftp server feature
* In windows search for "Turn Windows features On or Off" 
* Under the "Internet Information Services" section, make sure that "FTP Service" and "IIS Management Console" are enabled

### Create an FTP site in IIS
* Right click on "Sites" and click "Add FTP site"
* Enter a name and select the physical path to host in the FTP server and click next
* Select SSL certificate if required and click next
* Select Authentication as Basic, select allow access to all users or specific users and select both read and write permissions and click finish
* Now FTP server is setup
* You can start/stop the ftp server by right clicking on the site in the Sites section
* You can change setting like authentication, authorization easily by double clicking on the FTP site under the Sites section in left pane 

### Create an FTP site using Filezilla Server
* Download Filezilla server at https://filezilla-project.org/download.php?type=server
* Run the executable and complete the installation. While installation, set the server administration password and remember the server administration port
* After installation search for the application "Administer Filezilla server" and click
* 

## Installing DBeaver plugins without internet
### Step 1 - Download the database plugin jar files in a computer with internet  
* All the installed database plugins can be found in the folder
```C:\Users\<username>\AppData\Roaming\DBeaverData\drivers\maven\maven-central```
* On the Top Menu bar go to Database -> Driver Manager menu
* Then select the database you would like to connect and click edit
* In the pop up window, click Download/Update button. Now all the driver jar files will be downloaded in the computer from the internet
* After the drivers are downloaded, the folder location of jar file will be displayed on hovering the mouse over the library
* Go to the database plugins folder and copy all the jar files corresponding to the required database driver and paste in the computer without internet

### Step 2 - Installing the jar files in the computer without internet
* Open Database -> Driver Manager Menu
* Click "New" button and fill the input fields for the required database driver
* Click the "Add File" button to import all the jar files required for this database driver
* Now we have completed the offline installation of a database driver!

 The screenshots of the settings of common database drivers can be seen in the images below. You can take a snapshot of the driver settings from the computer that has the required database driver already installed and working.
 
 ![dbeaver_postgres_driver_settings](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/dbeaver_postgres_driver_settings.png)
 ![dbeaver_mysql_driver_settings](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/dbeaver_mysql_driver_settings.png)
 ![dbeaver_oracle_driver_settings](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/dbeaver_oracle_driver_settings.png)
 ![dbeaver_sqlite_driver_settings](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/dbeaver_sqlite_driver_settings.png)
 ### Video
The video for this post can be found [here](https://youtu.be/QvW1TBpimcs)

<iframe width="560" height="315" src="https://www.youtube.com/embed/QvW1TBpimcs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
 
### References
* DBeaver download - https://dbeaver.io/download/
* DBeaver site - https://dbeaver.io
* Installing a new JDBC database driver in DBeaver - https://dbeaver.com/docs/wiki/Database-drivers/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbOTk0NDk3OTI5LC0yMjgwODAxOTYsMzU3MT
c2OTMwXX0=
-->