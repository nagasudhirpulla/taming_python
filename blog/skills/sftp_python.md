
## Skill - SFTP server communication with pysftp python module

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>

* In this post we try to learn how to use `pysftp` python module to interact with SFTP server
* pysftp module can be used for SFTP server interactions like upload files, download files, read list of file names etc
* If you want to setup a local SFTP server, you can read my blog post [here](https://nagasudhir.blogspot.com/2022/03/setup-sftp-server-and-sftp-client-in.html)
 
## Connect to an FTP server
The following parameters are required to establish a connection to an SFTP server
* SFTP server host address (like "localhost" or "192.87.34.1" or "mysftp.abcd.com")
* SFTP server port (usually is 22)
* username
* password (if password authentication is used)
* private key file path (if private key authentication is used)

### Private key authentication
```python
import pysftp

# create connection options object and ignore known hosts check
cnopts = pysftp.CnOpts()
cnopts.hostkeys = None

# connection parameters
sftpHost = 'localhost'
sftpPort = 22
uname = 'Abcd'
privateKeyFilePath = 'C:/path/to/id_rsa'

# establish connection
with pysftp.Connection(sftpHost, port=sftpPort, username=uname, private_key=privateKeyFilePath, cnopts=cnopts) as sftp:
    print("connected to sftp server!")
```
* The path of private key file should be specified in `privateKeyFilePath` variable
* If you want to ignore known hosts checking, set `hostKeys` attribute as `None` in connection options
* Since we are using `with` statement while creating the connection object, the connection object will be automatically disposed

### Password based Authentication
```python
import pysftp

# create connection options object and ignore known hosts check
cnopts = pysftp.CnOpts()
cnopts.hostkeys = None

# connection parameters
sftpHost = 'localhost'
sftpPort = 22
uname = 'Abcd'
pwd = 'pwd@123'

# establish connection
with pysftp.Connection(sftpHost, port=sftpPort, username=uname, password=pwd, cnopts=cnopts) as sftp:
    print("connected to sftp server!")
```

## Change working directory using 'cwd'
```python
## ... code to connect to sftp server

# change working directory to a different folder
sftp.cwd("folder1/abcd")

# print current working directory
print(sftp.pwd)

# ... do something
```

## Get the list of filenames in remote folder using 'listdir'
```python
import pysftp
cnopts = pysftp.CnOpts()
cnopts.hostkeys = None
with pysftp.Connection('localhost', username='Abcd', private_key='./id_rsa', cnopts=cnopts) as sftp:
    # get list of filenames in current working directory
    fnames = sftp.listdir()
    print(fnames)

    # get list of filenames in any remote folder
    fnames = sftp.listdir("./remoteFolder")
    print(fnames)

    # get metadatas of files in remote server using listdir_attr
    fInfos = sftp.listdir_attr()
    print(fInfos)
```
* `listdir` function can be used to get the filenames in server folder
* `listdir_attr` function can be used to get the metadata of all files in server folder as SFTPAttribute objects

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
* pysftp cookbook - https://pysftp.readthedocs.io/en/release_0.2.9/cookbook.html#pysftp-connection
* pysftp docs - https://pysftp.readthedocs.io/en/release_0.2.9/pysftp.html
* paramiko docs - https://docs.paramiko.org/en/latest/api/sftp.html


<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIyOTEzMDgwNSwtNDcxMTk5ODQyLDEyNT
U1MTIyNTddfQ==
-->