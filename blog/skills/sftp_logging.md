## Skill - Logging in SFTP server in windows

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup SFTP server and SFTP client in Windows using OpenSSH server and WinSCP](https://nagasudhir.blogspot.com/2022/03/setup-sftp-server-and-sftp-client-in.html)

Go through the above skills if necessary for reference or revision
<hr/>

* In this post we will try to setup logging in a windows OpenSSH based SFTP server

* Logging can be controlled using the `sshd_config` file located in the `C:\ProgramData\ssh` folder

## Logging level
* Logging level can be any one among `QUIET, FATAL, ERROR, INFO, VERBOSE, DEBUG, DEBUG1, DEBUG2, and DEBUG3`
* More logs will be generated as the logging level goes from left to right in the above list
* The default logging level is INFO

### References
* OpenSSH SFTP server installation guide - https://winscp.net/eng/docs/guide_windows_openssh_server
* OpenSSH SFTP server official installation guide - https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse
* WinSCP - https://winscp.net/eng/download.php

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc5MTUzNzQ2NCw1NzkyMjE4Nl19
-->