## Skill - get latest file from ftp server folder using ftplib

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>

* In this post we try to learn how to get the latest file from a folder of an ftp server using python ftplib module
* ftplib is an inbuilt python module that can be used for FTP server interactions like upload files, download files, read list of file names etc
* A blogpost on how to setup a local FTP server can can be found [here](https://nagasudhir.blogspot.com/2022/02/setup-ftp-server-and-ftp-client-in.html)
* A blogpost on using ftplib python module can be found [here](https://nagasudhir.blogspot.com/2022/02/ftp-server-communication-with-ftplib.html)
 
## using mlsd command
* The best way to get the latest file of an ftp server folder using ftplib python module is the `mlsd` command
* But all ftp servers do not support msld command. For example filezilla FTP server supports this command and IIS based FTP server does not support this command
```py
from ftplib import FTP
ftp = FTP(host="127.0.0.1", user="abcd", passwd="testPass")

ftp.cwd("/folder1")

latestFile = None

for fInfo in ftp.mlsd(facts=["type", "modify", "size"]):
    # print(fInfo)
    if fInfo[1]["type"] == "file":
        if latestFile != None:
            if float(fInfo[1]["modify"]) >= float(latestFile[1]["modify"]):
                latestFile = fInfo
        else:
            latestFile = fInfo

# print(latestFile)
print(f"The latest file name is - {latestFile[0]}")
```


## using  nlst and mdtm
* The following approach can be adopted to find the latest file in ftp server with ftplib python module if nlst and mdtm commands are supported by the ftp server
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
print("execution complete...")
```

### With SSL
* While connecting to FTP server using SSL, use `FTP_TLS` instead of `FTP` function
* Also we need to call `ftp.prot_p()` to secure the connection after logging in
```python
import ftplib

# connection parameters
ftpHost = 'localhost'
ftpPort = 21
ftpUname = 'uname'
ftpPass = 'pass'

# create an FTP client instance, use the timeout(seconds) parameter for slow connections only
ftp = ftplib.FTP_TLS(timeout=30)

# connect to the FTP server
ftp.connect(ftpHost, ftpPort)

# login to the FTP server
ftp.login(ftpUname, ftpPass)

# setup secure data connection
ftp.prot_p()

# do something with the ftp client like upload, download etc

# send QUIT command to the FTP server and close the connection
ftp.quit()
print("execution complete...")
```

## Change working directory using 'cwd'
```python
## ... code to connect to ftp server

# change working directory to a different folder
ftp.cwd("folder1/abcd")

# ... do something
```

## Get the list of filenames in a folder using 'nlst'
In the below python script, we have created a function that fetches the list of filenames from the desired FTP server directory.
```python
import ftplib

def getFtpFilenames(ftpHost, ftpPort, ftpUname, ftpPass, remoteWorkingDirectory):
    # create an FTP client instance, use the timeout(seconds) parameter for slow connections only
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
print(fnames)
print("execution complete...")
```
You can copy this function and directly use it in your projects

## Upload files to FTP server directory using 'storbinary'
In the below python script, we have created a function that uploads a local file into the desired FTP server directory.
```python
import ftplib
import os

def uploadFileToFtp(localFilePath, ftpHost, ftpPort, ftpUname, ftpPass, remoteWorkingDirectory):
    # initialize the flag that specifies if upload is success
    isUploadSuccess: bool = False

    # extract the filename of local file from the file path
    _, targetFilename = os.path.split(localFilePath)

    # create an FTP client instance, use the timeout parameter for slow connections only
    ftp = ftplib.FTP(timeout=30)

    # connect to the FTP server
    ftp.connect(ftpHost, ftpPort)

    # login to the FTP server
    ftp.login(ftpUname, ftpPass)

    # change current working directory if specified
    if not (remoteWorkingDirectory == None or remoteWorkingDirectory.strip() == ""):
        _ = ftp.cwd(remoteWorkingDirectory)

    # Read file in binary mode
    with open(localFilePath, "rb") as file:
        # upload file to FTP server using storbinary, specify blocksize(bytes) only if higher upload chunksize is required
        retCode = ftp.storbinary(f"STOR {targetFilename}", file, blocksize=1024*1024)

    # send QUIT command to the FTP server and close the connection
    ftp.quit()

    # check if upload is success using the return code (retCode)
    if retCode.startswith('226'):
        isUploadSuccess = True

    # return the upload status
    return isUploadSuccess

# connection parameters
ftpHost = 'localhost'
ftpPort = 21
ftpUname = 'uname'
ftpPass = 'pass'
localFile = 'test.txt'
remoteFolder = "folder1/abcd"

# upload file
isUploadSuccess = uploadFileToFtp(localFile, ftpHost, ftpPort, ftpUname, ftpPass, remoteFolder)

print("upload status = {0}".format(isUploadSuccess))
```
* This function can be copied and used directly in your projects
* We can modify this function to for uploading multiple files into the FTP server using a `for` loop inside the function

## Download files from FTP server directory using 'retrbinary'
In the below python script, we have created a function that downloads files from FTP server into a local directory.
```python
import ftplib
import os


def downloadFilesFromFtp(localfolderPath, targetFilenames, ftpHost, ftpPort, ftpUname, ftpPass, remoteWorkingDirectory):
    # initialize the flag that specifies if download is success
    isDownloadSuccess: bool = False

    # create an FTP client instance, use the timeout parameter for slow connections only
    ftp = ftplib.FTP(timeout=30)

    # connect to the FTP server
    ftp.connect(ftpHost, ftpPort)

    # login to the FTP server
    ftp.login(ftpUname, ftpPass)

    # change current working directory if specified
    if not (remoteWorkingDirectory == None or remoteWorkingDirectory.strip() == ""):
        _ = ftp.cwd(remoteWorkingDirectory)

    # iterate through each remote filename and download
    for fItr in range(len(targetFilenames)):
        targetFilename = targetFilenames[fItr]
        # derive the local file path by appending the local folder path with remote filename
        localFilePath = os.path.join(localfolderPath, targetFilename)
        print("downloading file {0}".format(targetFilename))
        # download FTP file using retrbinary function
        with open(localFilePath, "wb") as file:
            retCode = ftp.retrbinary("RETR " + targetFilename, file.write)

    # send QUIT command to the FTP server and close the connection
    ftp.quit()

    # check if download is success using the return code (retCode)
    if retCode.startswith('226'):
        isDownloadSuccess = True
    return isDownloadSuccess


# connection parameters
ftpHost = 'localhost'
ftpPort = 21
ftpUname = 'uname'
ftpPass = 'pass'
localFolderPath = ""
remoteFolder = "folder1/abcd"
remoteFilenames = ["rguj.docx"]

# run the function to download the files from FTP server
isDownloadSuccess = downloadFilesFromFtp(
    localFolderPath,remoteFilenames, ftpHost, ftpPort, ftpUname, ftpPass, remoteFolder)

print("download status = {0}".format(isDownloadSuccess))
```
* This function can be copied and used directly in your projects
* We can modify this function as per our requirements like specifying local filenames etc.

## Other important FTP actions
All the important python ftp functions for directory listing, rename, delete file, delete folder, create folder, get the size of files etc. can be found at https://docs.python.org/3/library/ftplib.html#ftplib.FTP.dir

**ftp.dir(argument[, ...])**
Produce a directory listing as returned by the LIST command, printing it to standard output. The optional argument is a directory to list (default is the current server directory). Multiple arguments can be used to pass non-standard options to the LIST command. If the last argument is a function, it is used as a callback function as for retrlines(); the default prints to sys.stdout. This method returns None.

**ftp.rename(fromname, toname)**
Rename file fromname on the server to toname.

**ftp.delete(filename)**
Remove the file named filename from the server. If successful, returns the text of the response, otherwise raises error_perm on permission errors or error_reply on other errors.

**ftp.cwd(pathname)**
Set the current directory on the server.

**ftp.mkd(pathname)**
Create a new directory on the server.

**ftp.pwd()**
Return the pathname of the current directory on the server.

**ftp.rmd(dirname)**
Remove the directory named dirname on the server.

**ftp.size(filename)**
Request the size of the file named filename on the server. On success, the size of the file is returned as an integer, otherwise None is returned. Note that the SIZE command is not standardized, but is supported by many common server implementations.

### Video
Video for this post can be found [here](https://youtu.be/ME37cs7R0N0)

<iframe width="560" height="315" src="https://www.youtube.com/embed/ME37cs7R0N0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* Official ftplib documentation - https://docs.python.org/3/library/ftplib.html


<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQyMDEyMDQzMCwtMTQxNDI0NzAyMywtMT
U1NTU4MjQ5NCwtMTM0NDU2ODgwMSwtODM0NjI4MTQzLC0xMDUx
ODc4NzgwLC0xNTEwNjg5NjQzXX0=
-->