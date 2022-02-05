## Skill - Setup ftp server and client in Windows using IIS, Filezilla server and WinSCP

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>

In this post we will try to setup a local ftp server using IIS or Filezilla server and ftp client using WinSCP

## Setup FTP server
### Option 1 - Setup FTP server using IIS in windows
#### Step 1 - Enable IIS ftp server feature
* In windows search for "Turn Windows features On or Off" 
* Under the "Internet Information Services" section, make sure that "FTP Service" and "IIS Management Console" are enabled

#### Step 2 - Create an FTP site in IIS
* Right click on "Sites" and click "Add FTP site"
* Enter a name and select the physical path to host in the FTP server and click next
* Select SSL certificate if required and click next
* Select Authentication as Basic, select allow access to all users or specific users and select both read and write permissions and click finish
* Now FTP server is setup
* You can start/stop the ftp server by right clicking on the site in the Sites section
* You can change setting like authentication, authorization easily by double clicking on the FTP site under the Sites section in left pane 

### Option 2 - Setup FTP server using Filezilla Server
* Download Filezilla server at https://filezilla-project.org/download.php?type=server
* Run the executable and complete the installation. While installation, set the server administration password and remember the server administration port
* After installation search for the application "Administer Filezilla server" and click "Connect to Filezilla FTP Server"
* Enter the host, port and password click OK to connect to server
* In the top menu bar, open the Server->Configure menu
* In the Users left pane section, add a user, configure the virtual and native path for that user and set read and write access permissions for that user. Example Virtual path can be "/" and example Native path can be "C:\Users\xyz\Downloads\ftpFolder"
* Now the ftp server along with user logins is setup

## Setup FTP client in windows using WinSCP
* Download WinSCP at https://winscp.net/eng/download.php
* Run the downloaded executable file and complete the installation
* 

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
eyJoaXN0b3J5IjpbLTIwNTY5ODUzODAsOTk0NDk3OTI5LC0yMj
gwODAxOTYsMzU3MTc2OTMwXX0=
-->