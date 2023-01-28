## Skill - Setup Ubuntu or similar Linux distributions in Windows using WSL (Windows Subsystem for Linux)

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>

In this post we will install **WSL (Windows Subsystem for Linux)** in Windows to run Linux OS or Linux commands directly from Windows

## What is WSL
WSL (Windows Subsystem for Linux) is a windows feature that can run Linux environments like Ubuntu inside windows OS without installing separate virtual machines or dual booting

## Why use WSL
There can be many use cases like
* Running the source code or servers in Linux environments
* Running applications or commands in Windows that are only available for Linux based OS

## Install WSL from command line
**Note:** WSL can be installed from command line only in newer versions of Windows 10 or Windows 11 ( Refer [here](https://learn.microsoft.com/en-us/windows/wsl/install) )
* Open a command line in administrator mode
* Run the command `wsl --install` and restart the computer. This will install WSL along with Ubuntu Linux distribution
* To install WSL without the default Ubuntu Linux distribution, run the command `wsl --install --no-distribution` instead

## Install 

## TODOs
* install from cmd with --no-distribution
* install manually in older windows versions
* wsl basic commands
* run bash commands using wsl prefix
* run open windows drives in linux using /mnt/c path 
* pass commands between windows command line and linux using the pipe operator "|"

 
### References
* Basic wsl commands reference - https://learn.microsoft.com/en-us/windows/wsl/basic-commands#install
* Install wsl from command line - https://learn.microsoft.com/en-us/windows/wsl/install
* wsl manual installation for older windows versions - https://learn.microsoft.com/en-us/windows/wsl/install-manual
* A post on useful wsl commands - https://adamtheautomator.com/windows-subsystem-for-linux/#Setting_WSL_Configuration_Items_at_Bootup_with_wslconf 

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQwMjkzNjEyNywzMzY4NTI4ODksNzE0Nz
U1Mzc0LDk4NDA2MTgwLC0yMDI5ODM2NDIyXX0=
-->