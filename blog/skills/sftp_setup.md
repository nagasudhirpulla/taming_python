## Skill - Setup SFTP server and SFTP client in Windows using OpenSSH server and WinSCP

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>

* In this post we will try to setup an SFTP server using OpenSSH server and setup FTP client using WinSCP

## Setup SFTP server using OpenSSH zip file in any Windows version 
* Goto https://github.com/PowerShell/Win32-OpenSSH/releases
* Download the OpenSSH-Win64.zip file from the latest release
* Extract the zip file contents to the folder `C:\Program Files\OpenSSH`
![open_ssh_extract_location](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/open_ssh_extract_location.png)
* Open a command prompt as Administrator and use the following command to change to openssh directory 
`cd "C:\Program Files\OpenSSH"`
* Run  the following command
`powershell.exe -ExecutionPolicy Bypass -File install-sshd.ps1`
![open_ssh_service_powershell_install](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/open_ssh_service_powershell_install.PNG)
* Now the `sshd` and `ssh-agent` windows services should be installed. This can be seen in the `services.msc` window
* Change the startup type to Automatic from Manual and start both the `sshd` and `sshd-agent` services. Since we have set the startup type as automatic, both the services will start automatically upon system startup.
![open_ssh_windows_services](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/open_ssh_windows_services.png)
* Create the appropriate firewall policy to expose the SFTP port 22 to local or remote systems if required
* Now SFTP server accepts connections using username and password authentication

## Setup SFTP server in newer versions of windows
* Click windows button and search for "manage optional features"
* Click on "add a feature" and search for OpenSSH server and install it
* Now Open SSH server and OpenSSH Authentication agent services should be installed in the `services.msc` window
* You ca right click and change the start up type of both the services as automatic if you want the services to start upon system start up
* Create the appropriate firewall policy to expose the SFTP port 22 to local or remote systems if required
* Now SFTP server accepts connections using username and password authentication

## Downsides of password based authentication in SFTP
* OS user credentials of the server operating system are to be shared with the SFTP client which is not desirable
* OS user password is to be changed to change the password of SFTP client
* OS user password will be transmitted over the network

## Benefits of using public key based authentication in SFTP
* This type of authentication is more robust and secure
* SFTP client need not know the OS user password
* Multiple clients can use different private keys for a single OS user
* Private key can be changed easily from time to time without changing the user's OS password
* Access of SFTP client can be easily revoked by just removing the client's public key from the authenticated list, without locking out or modifying the OS user account

## Setup public key based authentication in windows
### Step 1 - Create a public and private key pair
* Public and private keys can be generated using one of the below methods
* The public key will be added to a text file in the SFTP server
* The private key will be used by the client to get authenticated and establish a session with the SFTP server  
#### Method 1 (Preferred) - Using ssh-keygen.exe
* `ssh-keygen.exe` can be found inside the program files folder like  `C:\Program Files\OpenSSH`
* Open a command window in that folder and run ssh-keygen.exe. Press enter till the execution is complete as shown in the image below
![open_ssh_keygen](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/open_ssh_keygen.png)
* During the key generation process, password protection can be set to private key by entering a passphrase as shown in the above image. This ensures additional protection in case the private key is in wrong hands
* The public key will be saved as `C:\Users\<username>\.ssh\id_rsa.pub` and private key will be saved as `C:\Users\<username>\.ssh\id_rsa` 

#### Method 2 - Using puttygen.exe
* Download puttygen.exe from https://www.puttygen.com/download-putty#Download_PuTTY_073_for_Windows
* Run puttygen.exe, make sure the settings are as shown in the below image and click *Generate* button. Move the cursor over the blank area to generate randomness. Then the key generation process will be completed
* Before clicking the Generate button, Key passphrase can be entered if we desire to password protect the generated private key
* Click on the save public key and save private key buttons to save the public and private keys into files like `pblic_key` and `prv_key.ppk`

![puttygen](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/puttygen.PNG)
### Step 3 - Place the public key in the SFTP server
* In the SFTP server, use a text editor like notepad and open the `authorized_keys` file located at `‪C:\Users\<username>\.ssh\authorized_keys` . If the file is not present, create a new file at this location.
* Copy the text in the public key file (like `id_rsa.pub`) generated in the previous step and paste the text inside the `authorized_keys` file in a new line.
![open_ssh_authorized_keys](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/open_ssh_authorized_keys.png)* In this way, multiple public keys can be added one below the other in this text file so that they can be authenticated by the SFTP server
* Also note that `authorized_keys` file should **not** have any extension like .txt, .docx etc.

### Step 4 - Change the access control list (ACL) of the authorized_keys file in SFTP server
* The access control list (ACL) of `authorized_keys` file should be configured such that only `Administrators` and `System` users should have the access to this file
* To achieve this, open a command prompt as administrator and run the following command
```bat
icacls.exe "C:\Users\<username>\.ssh\authorized_keys" /inheritance:r /grant "Administrators:F" /grant "SYSTEM:F"
```
![open_ssh_authorized_keys_permissions](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/open_ssh_authorized_keys_permissions.png)* You can verify the access control list of the `authorized_keys` file by right click on file->properties->security tab as shown in the below image
![open_ssh_authorized_keys_properties](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/open_ssh_authorized_keys_properties.png)
### Step 5 - Edit the sshd_config file of the SFTP server to configure public key based authentication
* `sshd_config` file is located at `C:\ProgramData\ssh` folder of the SFTP server
* Open it with a text editor like Notepad or VS code
* Modify the `sshd_config` file to make sure the following lines are present in the file.
```bat
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
PasswordAuthentication no
PermitEmptyPasswords no
Subsystem sftp internal-sftp
Match User <username>
	X11Forwarding no
	AllowTcpForwarding no
	PermitTTY no
	ForceCommand internal-sftp
	PasswordAuthentication no
```
Replace `<username>` with the OS username
* Comment out the lines at the end with a `#` as shown below
```bash
#Match Group administrators
# AuthorizedKeysFile __PROGRAMDATA__/ssh/administrators_authorized_keys
```
## Restrict user to a folder (also called folder jailing)
* Using `ChrootDirectory` in sshd_config file, we can restrict the SFTP user to a particular folder. The user cannot navigate to any of the parent folders of the specified folder
* This is also called folder jailing. This adds extra security to the SFTP server
* To achieve folder jailing edit the `sshd_config` file located in the `C:\ProgramData\ssh` folder of SFTP server as shown below
```bash
Match User <username>
	ChrootDirectory ~/Pictures/Screenshots
	X11Forwarding no
	AllowTcpForwarding no
	PermitTTY no
	ForceCommand internal-sftp
	PasswordAuthentication no
```
* Due to `ChrootDirectory` used in sshd_config file, the SFTP user cannot navigate to any of the parent folders of `C:\Users\Nagasudhir\Pictures\Screenshots`

## Setup SFTP client in windows using WinSCP
* Download WinSCP at https://winscp.net/eng/download.php
* Run the downloaded executable file and complete the installation
* Open WinSCP app
* Click on New Session button in the top left menu
* Set protocol as SFTP, encryption as TLS/SSL explicit encryption if the FTP server uses encryption or select No encryption, port as 21, hostname as localhost, enter username and password. Finally click login
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
eyJoaXN0b3J5IjpbMjAxNTMwODM5MiwtMTAwNDA1MjA1NywtND
AwNTcyNzM2LC0xMDE0NTU2MjQ4LDI5ODk0NDA3OCw5ODAzMjU2
MDIsLTE1Njc2NjQwMzksLTE2MDA3NzI4NDAsLTYxNzM3NzU1MS
w1MzQ5OTI5MzQsLTE1MjY0NjI4NTksLTE0ODIyMzgxMDMsMTA1
MDczMDU5MywtODUzMDgzOCwtMTUyNTYyNjMwMiwzODE4ODU2Mz
ksMjE1MDUwOTE2LC03MjQ0Mzg5ODksLTE4Njg0NjMyMTMsNzY4
NDI4MDM3XX0=
-->