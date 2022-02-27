## Skill - Setup SFTP server and SFTP client in Windows using OpenSSH server and WinSCP

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>

* In this post we will try to setup an SFTP server using OpenSSH server and setup FTP client using WinSCP

## Setup SFTP server using OpenSSH zip file in any Windows version 
#### Step 1 - Download zip file from GitHub
* Goto https://github.com/PowerShell/Win32-OpenSSH/releases
* Download the OpenSSH-Win64.zip file from the latest release
* Extract the zip file contents to the folder `C:\Program Files\OpenSSH`
TODO Folder Image
* Open a command prompt as Administrator and use the following command to change to openssh directory 
`cd "C:\Program Files\OpenSSH"`
* Run  the following command
`powershell.exe -ExecutionPolicy Bypass -File install-sshd.ps1`
TODO command execution image
* Now the `sshd` and `ssh-agent` windows services should be installed. This can be seen in the `services.msc` window
TODO windows background services image
* Change the startup type to Automatic from Manual and start both the sshd and sshd-agent services. Since we have set the startup type as automatic, both the services will start automatically upon system startup

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
 
### Video
Video for this post can be found [here](https://youtu.be/6gHlAfviiPM)

<iframe width="560" height="315" src="https://www.youtube.com/embed/6gHlAfviiPM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* OpenSSH SFTP server installation guide - https://winscp.net/eng/docs/guide_windows_openssh_server
* OpenSSH SFTP server official installation guide - https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse
* WinSCP - https://winscp.net/eng/download.php

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgyODE4MjUwNSwtMTAwNzA1MjY0N119
-->