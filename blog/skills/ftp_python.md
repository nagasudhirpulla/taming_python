## Skill - FTP server communication with ftplib python module

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>

* In this post we try to learn how to use `ftplib` python module to communicate with FTP server
* ftplib is an inbuilt python module that can be used for FTP server interactions like upload files, download files, read list of file names etc
* If you want to setup a local FTP server, you can read my blog post [here](https://nagasudhir.blogspot.com/2022/02/setup-ftp-server-and-ftp-client-in.html) 
 
## Connect to an FTP server
The following paramerters are required to establis
```python
import ftplib

# connection parameters
ftpHost = 'localhost'
ftpPort = 21
ftpUname = 'uname'
ftpPass = 'pass'

# create an FTP client instance, use the timeout parameter for slow connections only
ftp = ftplib.FTP(timeout=30)

# connect to the FTP server
ftp.connect(ftpHost, ftpPort)

# login to the FTP server
ftp.login(ftpUname, ftpPass)

# do something with the ftp client like upload, download etc

# send QUIT command to the FTP server and close the connection
ftp.quit()
```
 
### References
* Official ftplib documentation - https://docs.python.org/3/library/ftplib.html


<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYwODgxMDAyMSw3ODk0NDQ3NjNdfQ==
-->