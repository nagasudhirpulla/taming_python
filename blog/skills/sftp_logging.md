## Skill - Logging in SFTP server in windows

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup SFTP server and SFTP client in Windows using OpenSSH server and WinSCP](https://nagasudhir.blogspot.com/2022/03/setup-sftp-server-and-sftp-client-in.html)

Go through the above skills if necessary for reference or revision
<hr/>

* In this post we will try to setup logging in a windows OpenSSH based SFTP server

* Logging can be controlled using the `sshd_config` file located in the `C:\ProgramData\ssh` folder

## Logging level
* Logging level controls the minimum criticality level which the logs will be generated 
* Logging level can be any one among `QUIET, FATAL, ERROR, INFO, VERBOSE, DEBUG, DEBUG1, DEBUG2, and DEBUG3`
* More number of logs will be generated as the logging level goes from left to right in the above list
* The default logging level is INFO

## Logging facility
* Logging facility controls the location of logging
* Logging facility can be any one among `DAEMON, USER, AUTH, LOCAL0, LOCAL1, LOCAL2, LOCAL3, LOCAL4, LOCAL5, LOCAL6, LOCAL7`
* The default logging facility is `AUTH` which sends the logs to Windows Events (ETW). Logs can be seen from Windows `Event Viewer`
* To send logs to a file, the logging facility should be `LOCAL0` . Logs be found in `C:\ProgramData\ssh\logs\sshd.log` file

## Logging level and Logging facility in sssh

### References
* OpenSSH logging official documentation - https://github.com/PowerShell/Win32-OpenSSH/wiki/Logging-Facilities
* OpenSSH SFTP server installation guide - https://winscp.net/eng/docs/guide_windows_openssh_server
* OpenSSH SFTP server official installation guide - https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMzkyNzAzNTQsNTc5MjIxODZdfQ==
-->