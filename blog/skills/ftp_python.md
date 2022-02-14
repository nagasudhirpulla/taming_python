## Skill - FTP server communication with ftplib python module

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>

* In this post we try to learn how to use `ftplib` python module to communicate with FTP server
* ftplib is an inbuilt python module that can be used for FTP server interactions like upload files, download files, read list of file names etc
* If you want to setup a local FTP server, you can read my blog post [here](https://nagasudhir.blogspot.com/2022/02/setup-ftp-server-and-ftp-client-in.html) 
 
## Connect to an FTP server
The following parameters are required to establish a connection to an FTP server
* FTP server host address (like "localhost" or "192.87.34.1" or "myftp.abcd.com")
* FTP server port (usually is 21)
* username
* password

```python
import ftplib

# connection parameters
ftpHost = 'localhost'
ftpPort = 21
ftpUname = 'uname'
ftpPass = 'pass'

# create an FTP client instance, use the timeout(seconds) parameter for slow connections only
ftp = ftplib.FTP(timeout=30)

# connect to the FTP server
ftp.connect(ftpHost, ftpPort)

# login to the FTP server
ftp.login(ftpUname, ftpPass)

# do something with the ftp client like upload, download etc

# send QUIT command to the FTP server and close the connection
ftp.quit()
```

## Change working directory with 'cwd' function
```python
## ... code to connect to ftp server

# change working directory to a different folder
ftp.cwd("folder1/abcd")

# ... do something
```

## Get the list of filenames in a folder
In the below python script, we have created a 
```python
import ftplib

def getFtpFilenames(ftpHost, ftpPort, ftpUname, ftpPass, remoteWorkingDirectory):
    # create an FTP client instance, use the timeout parameter for slow connections only
    ftp = ftplib.FTP(timeout=30)
    
    # connect to the FTP server
    ftp.connect(ftpHost, ftpPort)
    
    # login to the FTP server
    ftp.login(ftpUname, ftpPass)

    # change current working directory if specified
    if not (remoteWorkingDirectory == None or remoteWorkingDirectory.strip() == ""):
        _ = ftp.cwd(remoteWorkingDirectory)
    
    # initialize the filenames as an empty list
    fnames = []
    
    try:
        # use nlst function to get the list of filenames
        fnames = ftp.nlst()
    except ftplib.error_perm as resp:
        if str(resp) == "550 No files found":
            fnames = []
        else:
            raise
    
    # send QUIT command to the FTP server and close the connection
    ftp.quit()

    # return the list of filenames
    return fnames

# connection parameters
ftpHost = 'localhost'
ftpPort = 21
ftpUname = 'uname'
ftpPass = 'pass'
fnames = getFtpFilenames(ftpHost, ftpPort, ftpUname, ftpPass, "folder1/abcd")
```
 
### References
* Official ftplib documentation - https://docs.python.org/3/library/ftplib.html


<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk1ODkyNjk1MywtMTk0NjE4ODA4OCwyMD
IwNjg1NjAwLDc4OTQ0NDc2M119
-->