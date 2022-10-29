## Skill - SFTP server in Windows with multiple users and read-only option

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup SFTP server and SFTP client in Windows using OpenSSH server and WinSCP](https://nagasudhir.blogspot.com/2022/03/setup-sftp-server-and-sftp-client-in.html)
* [Setup SFTP server and SFTP client in Windows using OpenSSH server and WinSCP](https://nagasudhir.blogspot.com/2022/10/setup-logging-for-sftp-server-in-windows.html)

Go through the above skills if necessary for reference or revision
<hr/>

* In this post we will try to setup windows OpenSSH based SFTP server with multiple users and read-only option

* User logins can be controlled using the `sshd_config` file located in the `C:\ProgramData\ssh` folder
* The read-only access can be controlled at the Operating System level

## Setup SFTP for multiple users
### Step 1: Create a new user account (if required)
* New user can be created in windows by searching for "Add, edit, or remove other users" in system settings or windows search

### Step 2: Modify sshd_config file for providing access to the user
* Create a section in `sshd_config` file located in the folder `C:\ProgramData\ssh` as shown below
```bash
Match User james
	ChrootDirectory "~/Downloads"
	X11Forwarding no
	AllowTcpForwarding no
	PermitTTY no
	ForceCommand internal-sftp
	PasswordAuthentication no
	PubkeyAuthentication yes
```
* In the above example, a section is created in the `sshd_config` file for the user `james`
* `PasswordAuthentication` and `PubkeyAuthentication` can be set as per requirement
* `ChrootDirectory` in this example is `~/Downloads`, which means the full path would be `C:\Users\James\Downloads`. In this way `~` can be used to express the SFTP root folder path relative to the user directory. However absolute path can also be set like `ChrootDirectory "C:\Users\John\Documents\test"` , provided the windows user `james` has at-least read access access to the folder  `C:\Users\John\Documents\test`

### Step 3: Setup authorized_keys file in .ssh folder of the user (for private key authentication)
* If a user is to be authenticated using private key based authentication, the corresponding public key should be kept in a new line of the  `authorized_keys` file inside the `C:\Users\<username>\.ssh` folder.
*   The access control list (ACL) of `authorized_keys` file should be configured such that only `Administrators` and `System` users should have the access to this file
*   To achieve this, open a command prompt as administrator and run the following command

```bash
icacls.exe "C:\Users\James\.ssh\authorized_keys" /inheritance:r /grant "Administrators:F" /grant "SYSTEM:F"
``` 

* You can verify the access control list of the `authorized_keys` file by right click on file->properties->security tab as shown in the below image
![open_ssh_authorized_keys_properties.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/open_ssh_authorized_keys_properties.png)
* Not ensuring the permissions of the `authorized_keys` file will fail the login attempts, hence it is important. Login failures due to wrong file permissions of `authorized_keys` file will be logged in the SFTP server logs. Check out [this blog post](https://nagasudhir.blogspot.com/2022/10/setup-logging-for-sftp-server-in-windows.html) to know how to see SFTP server logs.

## Setup Read-only file access to SFTP user
* For this example, let us setup Read-only SFTP folder for a windows user `james`
* Take a folder which is outside `C:\Users\james`, for example `C:\Users\otheruser\Documents\reports`
* Share the folder with only read-access to the user `james`
![sftp_readonly_folder_sharing.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/sftp_readonly_folder_sharing.png)
* In `sshd_config` file, set the `ChrootDirectory` to the above folder. For example, 
```
ChrootDirectory "C:\Users\otheruser\Documents\reports"
```



<hr/>

### References
* OpenSSH logging official documentation - https://github.com/PowerShell/Win32-OpenSSH/wiki/Logging-Facilities
* OpenSSH SFTP server installation guide - https://winscp.net/eng/docs/guide_windows_openssh_server
* OpenSSH SFTP server official installation guide - https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse



[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3MjY2NDkwNzgsMjU0MjAxNDIzLC02NT
Y1MTY3ODQsLTE4MDE1NjM3NCw3NzY4OTMyODQsNTE0NTE0MzQ0
LC0xMTg2MjkxMDczLC0zNzgwNjE3NzAsMTY4NDk1ODg0MSwtNT
AxMjczNTAsLTUzMjM2MjUyM119
-->