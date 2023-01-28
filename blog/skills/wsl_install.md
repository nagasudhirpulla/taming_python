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

## Install WSL in older Windows 10 versions
* In some older windows 10 versions, WSL installation with `wsl --install` may not be possible.
* For such scenarios, refer to the manual installation steps as per the Microsoft documentation [here](https://learn.microsoft.com/en-us/windows/wsl/install-manual)

## Install a Linux distribution from command line
* Get the list of available Linux distributions using the command `wsl --list --online` or `wsl -l -o` .  A list of available distributions will be displayed. 
For example 
```
The following is a list of valid distributions that can be installed.
Install using 'wsl --install -d <Distro>'.

NAME               FRIENDLY NAME
Ubuntu             Ubuntu
Debian             Debian GNU/Linux
kali-linux         Kali Linux Rolling
SLES-12            SUSE Linux Enterprise Server v12
SLES-15            SUSE Linux Enterprise Server v15
Ubuntu-18.04       Ubuntu 18.04 LTS
Ubuntu-20.04       Ubuntu 20.04 LTS
Ubuntu-22.04       Ubuntu 22.04 LTS
OracleLinux_8_5    Oracle Linux 8.5
OracleLinux_7_9    Oracle Linux 7.9
```
* Choose a distribution by the `NAME` and install using the command `wsl --insall -d <NAME>`. For example, based on the above output, you can run `wsl --insall -d kali-linux` to install Kali Linux distribution

## Install a Linux distribution from Microsoft store
* Open Microsoft store app in Windows
* Search for a linux distribution like "Ubuntu", "Kali Linux", "Debian" etc.
* Install the Linux distribution from Microsoft store

## List out the installed Linux distributions
* In a command line, run the command `wsl --list --verbose` or `wsl -l -v` to see the list of installed wsl distributions and their status 

## Update WSL kernel
* WSL kernel can be updated from command line using the command `wsl --update` . However by WSL will update automatically with windows update 

## Open a specific WSL distribution
* First view the list of installed Linux distributions using the command `wsl -l -v`
* Then open the desired distribution with the command `wsl -d <distroName>`, where "distroName" is the name of the installed Linux distribution

## Update a WSL Linux distribution
* Open the Linux distribution from start menu or with the command `wsl`
* If a Debian based Linux distribution like Ubuntu is installed, then it can be updated using the command `sudo apt update && sudo apt upgrade` 
* Now the packages in the Linux distribution will be updated

## Uninstall a Linux distribution
* First view the list of installed Linux distributions using the command `wsl -l -v`
* Then run the command `wsl --unregister <distroName>` where "distroName" is the name of the Linux distribution to be uninstalled
* Alternatively, a Linux distribution can also be manually uninstalled from "Add or remove programs" section in the System Settings

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
eyJoaXN0b3J5IjpbLTgyMDEzMTQzLC00NjI1NzI5ODksNjIxNj
c2NDM3LC0xMDM5Njg0OTkyLC00MDI5MzYxMjcsMzM2ODUyODg5
LDcxNDc1NTM3NCw5ODQwNjE4MCwtMjAyOTgzNjQyMl19
-->