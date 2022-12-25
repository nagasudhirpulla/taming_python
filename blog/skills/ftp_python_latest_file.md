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
# connect to ftp server
ftp = FTP(host="127.0.0.1", user="abcd", passwd="testPass")

# change working directory as requried
ftp.cwd("/folder1")

# initialize the latest file info
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
* The following approach can be adopted to find the latest file in ftp server with ftplib python module if `nlst` and `mdtm` commands are supported by the ftp server
* `nlst` command returns the list of all the filenames and folders in a remote folder and `mdtm` returns the modified time information for a specified remote file name
* running `mdtm` command on a remote folder instead of a file will return an error in some servers like IIS based FTP server
* One downside of using `nlst` is that the information whether the filename is file or folder is not known. This needs to be determined separately. Windows IIS FTP server throws error when `mdtm` command on a folder. So try-except block is used in the below example while using `mdtm` command

```python
from ftplib import FTP
# connect to ftp server
ftp = FTP(host="127.0.0.1", user="admin", passwd="testPass")

# change the working directory if requried
ftp.cwd("/folder1")

# initialize the latest file info
latestFileTime = None
latestFilename = None

for fName in ftp.nlst():
    # print(fName)
    # mdtm may not be supported for folder is IIS based FTP server, so wrapping with try except
    try:
        fTimeInfo = ftp.voidcmd(f"MDTM {fName}")
        fTime = fTimeInfo.split(" ")[1]
        if latestFileTime!=None:
            if fTime >= latestFileTime:
                latestFileTime = fTime
                latestFilename = fName
        else:
            latestFileTime = fTime
            latestFilename = fName
    except:
        print(f"error while processing {fName}")

# print(latestFile)
print(f"The latest file name is - {latestFilename}")

```

## using dir command
* If none of the above approaches are working, then the string returned by the `dir` command can be used to parse the file names and modification times to determine the latest file name
* The string returned by the `dir` command is dependent in the FTP server implementation. For example, `dir` command output of IIS based FTP server is different from that of Filezilla based FTP server.

```python
from ftplib import FTP
# connect to ftp server
ftp = FTP(host="127.0.0.1", user="Nagasudhir", passwd="wrldc@123")

# change working directory as requried
ftp.cwd("/lab/YarpTest")

folderInfo = ftp.dir()
print(folderInfo)

# parse the folder info output line by line to determine the latest file
```

### References
* Official ftplib documentation - https://docs.python.org/3/library/ftplib.html


<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbMzY3MDgxNTE1LC03NzAwMDAyMTcsMTg1Nj
cyMDE0OCwxMjYwMTI4NzkyLC01NzgxMzU4NDcsLTE0MTQyNDcw
MjMsLTE1NTU1ODI0OTQsLTEzNDQ1Njg4MDEsLTgzNDYyODE0My
wtMTA1MTg3ODc4MCwtMTUxMDY4OTY0M119
-->