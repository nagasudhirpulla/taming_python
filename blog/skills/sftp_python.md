## Skill - SFTP server communication with pysftp python module

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>

* In this post we try to learn how to use `pysftp` python module to interact with SFTP server
* pysftp module can be used for SFTP server interactions like upload files, download files, read list of file names etc
* If you want to setup a local SFTP server, you can read my blog post [here](https://nagasudhir.blogspot.com/2022/03/setup-sftp-server-and-sftp-client-in.html)
 
## Connect to an SFTP server
The following parameters are required to establish a connection to an SFTP server
* SFTP server host address (like `"localhost"` or `"192.87.34.1"` or `"mysftp.abcd.com"`)
* SFTP server port (usually is 22)
* username
* password (if password authentication is used)
* private key file path (if private key authentication is used)

### Private key authentication
```python
import pysftp

# create connection options object and ignore_known hosts check
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

# create connection options object and ignore known_hosts check
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

    # get metadatas of files in remote server using listdir_attr. Here we are printing the filename, mode, size in bytes, modified time of each file
    fInfos = sftp.listdir_attr()
    print([[f.filename, f.st_mode, f.st_size, f.st_mtime] for  f  in  fInfos])

print('execution complete!')
```

* `listdir` function can be used to get the filenames in server folder
* `listdir_attr` function can be used to get the metadata of all files in server folder as `SFTPAttribute` objects

## Upload files to SFTP server directory using 'put', 'put_d', 'put_r'
```python
import pysftp
cnopts = pysftp.CnOpts()
cnopts.hostkeys = None
with pysftp.Connection('localhost', username='Abcd', private_key='./id_rsa', cnopts=cnopts) as sftp:
    # upload file to current working directory of the sftp server
    # without changing the file modification time
    sftp.put('C:/path/to/abcd.txt', preserve_mtime=True)
    
    # upload file to different remote folder and file path
    sftp.put('xyz.txt', preserve_mtime=True, remotepath="./jgjhgajhsd/def.txt")

    # upload contents from local directory to remote directory
    sftp.put_d(r"C:\path\to\localFolder", "./remoteFolder", preserve_mtime=True)
    
    # upload contents from local directory to remote directory and create intermediate folders if required
    sftp.put_r(r"C:\path\to\localFolder", "./remoteFolder", preserve_mtime=True)
    
    print("copy completed!")
```
* `put` method can be used to upload single file to sftp server 
* `put_d` method can be used to upload all folder contents to sftp server folder
* `put_r` method can be used to upload all folder contents to sftp server folder along with sub-folders

## Download files from SFTP server directory using 'get', 'get_d', 'get_r'
```python
import pysftp
cnopts = pysftp.CnOpts()
cnopts.hostkeys = None
with pysftp.Connection('localhost', username='Abcd', private_key='./id_rsa', cnopts=cnopts) as sftp:
    # download remote file to current local folder
    sftp.get("./remoteFolder/khd.txt", preserve_mtime=True)

    # download remote file to a custom local folder and filename
    sftp.get("./remoteFolder/khd.txt", localpath="./test/abc.txt", preserve_mtime=True)

    # dowmload remote folder files to local folder
    sftp.get_d("./remoteFolder", localdir="./test", preserve_mtime=True)

    # dowmload remote folder along with sub folders recursively to local folder
    sftp.get_r("./remoteFolder", localdir="", preserve_mtime=True)
```

* `get` method can be used to download single file from remote server
* `get_d` method can be used to download remote folder contents to local folder
* `get_r` method can be used to download the remote folder directly to the local system along with sub-folders 

## Get Metadata of file using 'stat'
```python
import pysftp
import datetime as dt
cnopts = pysftp.CnOpts()
cnopts.hostkeys = None
with pysftp.Connection('localhost', username='Nagasudhir', private_key='./id_rsa', cnopts=cnopts) as sftp:
    # get the remote file metadata using stat function
    fstats = sftp.stat('./remFoldr/khd.txt')
    
    print(fstats.st_size) # size in bytes
    print(dt.datetime.fromtimestamp(fstats.st_mtime)) # recent modification time
    print(fstats.st_mode) # protection bits
    print(dt.datetime.fromtimestamp(fstats.st_atime)) # recent access time 
    print(fstats.st_uid) # user id of owner
    print(fstats.st_gid) # group id of owner
```

## Delete remote folder
* An empty folder in an SFTP server can be deleted easily using the `sftp.rmdir("./remoteFolder")` function but there is no straight forward function to delete a non-empty remote folder
* Hence we have created a function as shown below that deletes a non-empty remote SFTP folder by deleting the files first and then deleting the empty folder. The solution is based on a stack overflow post at https://stackoverflow.com/questions/20507055/recursive-remove-directory-using-sftp/20507586#20507586
```python
import os
from stat import S_ISDIR
import pysftp

def rm(sftp, path):
    files = sftp.listdir(path)
    for f in files:
        filepath = os.path.join(path, f)
        isDir = False
        try:
            isDir = S_ISDIR(sftp.stat(filepath).st_mode)
        except IOError:
            isDir = False
        if isDir:
            rm(sftp, filepath)
        else:
            sftp.remove(filepath)
    sftp.rmdir(path)

cnopts = pysftp.CnOpts()
cnopts.hostkeys = None
with pysftp.Connection('localhost', username='Abcd', private_key='./id_rsa', cnopts=cnopts) as sftp:
    # delete an empty remote folder
    # sftp.rmdir("remoteFolder")

    # delete a remote folder with contents
    rm(sftp, "./remoteFolder")
```
## Other important SFTP actions
All the important sftp functions for directory listing, rename, delete file, delete folder, create folder, get the size of files etc. can be found at https://pysftp.readthedocs.io/en/release_0.2.9/cookbook.html and https://pysftp.readthedocs.io/en/release_0.2.9/pysftp.html

**sftp.mkdirs(remotepath, mode=777)**
Create a new directory on the remote server. intermediate folders will also be created if required. On some systems mode is ignored

**sftp.stat(remotePath).st_size**
Request the size of the file or folder on the server in bytes.

**sftp.rename(_remote_src_, _remote_dest_)**
rename remote file or folder

**sftp.remove(remotefile)**
Remove the remote server file based on the file path provided

**sftp.cwd(remotepath)**
Set the current directory on the server.

**sftp.pwd**
Return the path of current directory on the server.

**sftp.rmdir(remotepath)**
Remove the directory named remotepath on the server. The directory should be empty for this function to successfully execute.

### References
* pysftp cookbook - https://pysftp.readthedocs.io/en/release_0.2.9/cookbook.html#pysftp-connection
* pysftp docs - https://pysftp.readthedocs.io/en/release_0.2.9/pysftp.html
* paramiko docs - https://docs.paramiko.org/en/latest/api/sftp.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU2NDMzNDI2MCwtMTA3MDIxNjYyNCwxMz
I3NTU4MTcyLDI2MTA5NzQxMiwtMTk1NTA3MjI5OCwxMDc2MDgw
NTE0LC0xMzQ0OTc0NTcwLC0xMDUxODU5MjE5LDEzNTQxOTcwMD
UsLTg1OTA3Njg1LDI4MTA2ODMxMiwtNTc1MjI2MzU4LC00NzEx
OTk4NDIsMTI1NTUxMjI1N119
-->