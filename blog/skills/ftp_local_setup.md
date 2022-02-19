## Skill - Setup FTP server and FTP client in Windows using IIS, Filezilla server and WinSCP

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>

* In this post we will try to setup a local FTP server using IIS or Filezilla server and setup FTP client using WinSCP
* Sometimes, we might want to test our code with out production FTP server using a local FTP server. This can be a use case for setting up a local FTP server and client

## Setup FTP server
### Option 1 - Setup FTP server using IIS in windows
#### Step 1 - Enable IIS ftp server feature
* In windows search for "Turn Windows features On or Off" 
* Under the "Internet Information Services" section, make sure that "FTP Service" and "IIS Management Console" are enabled

![iis_ftp_minimum_windows_features](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/iis_ftp_minimum_windows_features.PNG)
#### Step 2 - Create an FTP site in IIS
* Right click on "Sites" and click "Add FTP site"
* Enter a name and select the physical path to host in the FTP server and click next
![iis_add_ftp_site_1](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/iis_add_ftp_site_1.PNG)
* Select SSL certificate if required and click next
![iis_add_ftp_site_2](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/iis_add_ftp_site_2.PNG)
* Select Authentication as Basic, select allow access to all users or specific users and select both read and write permissions and click finish
![iis_add_ftp_site_3](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/iis_add_ftp_site_3.PNG)
* Now FTP server is setup
* You can start/stop the ftp server by right clicking on the site in the Sites section
![iis_add_ftp_site_4](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/iis_add_ftp_site_4.PNG)
* You can change setting like authentication, authorization easily by double clicking on the FTP site under the Sites section in left pane 

### Option 2 - Setup FTP server using Filezilla Server
* Download Filezilla server at https://filezilla-project.org/download.php?type=server
* Run the executable and complete the installation. While installation, set the server administration password and remember the server administration port
* After installation search for the application "Administer Filezilla server" and click "Connect to Filezilla FTP Server"
* Enter the host, port and password click OK to connect to server
![filezilla_server_admin_1](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/filezilla_server_admin_1.PNG)
* In the top menu bar, open the Server->Configure menu
![filezilla_server_admin_2](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/filezilla_server_admin_2.PNG)
* You can check the port bindings of the FTP server in the FTP Server left menu
![filezilla_server_admin_3](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/filezilla_server_admin_3.PNG) 
* In the Users left pane section, add a user, configure the virtual and native path for that user and set read and write access permissions for that user. Example Virtual path can be "/" and example Native path can be "C:\Users\xyz\Downloads\ftpFolder"
![filezilla_server_admin_4](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/filezilla_server_admin_4.PNG)
* Now the ftp server along with user logins is setup

## Setup FTP client in windows using WinSCP
* Download WinSCP at https://winscp.net/eng/download.php
* Run the downloaded executable file and complete the installation
* Open WinSCP app
* Click on New Session button in the top left menu
* Set protocal as FTP, encryption as TLS/SSL explicit encryption if the FTP server uses encryption or select No encryption, port as 21, hostname as localhost, enter username and password. Finally click login
![winscp_connect_ftp](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/winscp_connect_ftp.PNG)
* Now FTP server is connected to WinSCP
* We can copy,paste,rename,delete the ftp server files just like file explorer
![winscp_ui](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/winscp_ui.PNG)
 
### References
* IIS FTP server setup - https://winscp.net/eng/docs/guide_windows_ftps_server
* Filezilla server - https://filezilla-project.org/download.php?type=server
* WinSCP - https://winscp.net/eng/download.php

### Video
Video for this post can be found [here](https://youtu.be/6gHlAfviiPM)

<iframe width="560" height="315" src="https://www.youtube.com/embed/6gHlAfviiPM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAyOTU2OTY5NSwtNDc4ODYzMjQ3LC0xMz
M3MzUyMzk4LDE5NzIwMDE0MjYsLTE3Nzk0MDUyMzIsLTUzOTE1
ODQ1MSwxOTIwMDU4NTQwLDE5MjAwNTg1NDAsNjg5MDU2ODk0LC
0xNzMyMTc2MjA0LDk5NDQ5NzkyOSwtMjI4MDgwMTk2LDM1NzE3
NjkzMF19
-->