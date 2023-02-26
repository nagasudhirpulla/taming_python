## Skill - Run python on Linux in Windows using WSL and VS Code

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>

In this post we will learn
* Setting python in Ubuntu inside WSL
* Install multiple python versions using deadsnakes ppa
* Running python in WSL (Windows Subsystem for Linux)
* Visual Studio Code (VS Code) support for WSL
* Setting up virtual environments for python projects
* `update-alternatives` command for 

## What is WSL
WSL (Windows Subsystem for Linux) is a windows feature that can run Linux environments like Ubuntu inside windows OS without installing separate virtual machines or dual booting. A detailed post on setting up WSL in windows can be found [here](https://nagasudhir.blogspot.com/2023/01/setup-ubuntu-or-similar-linux.html) 

## Setup python, pip and virtual environments in Ubuntu
### Setting up python
* Python comes pre-installed in Ubuntu. It is accessible as `python3`
* Check if python is installed using `python3 --version`
* Check the installation location of python using `which python`
* Update all the packages using `sudo apt update && sudo apt upgrade`
* Update only python3 using `sudo apt upgrade python3`

### Setting up pip
* `pip` is useful for managing external packages in python
* Install pip using `sudo apt install python3-pip`

### Setting up venv for virtual environments 
* `venv` is useful for managing virtual environments in python
* Install venv using `sudo apt install python3-venv`
 

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
* Search for a Linux distribution like "Ubuntu", "Kali Linux", "Debian" etc.
* Install the Linux distribution from Microsoft store

## List out the installed Linux distributions
* In a command line, run the command `wsl --list --verbose` or `wsl -l -v` to see the list of installed WSL distributions and their status 

## Open a specific WSL distribution
* First view the list of installed Linux distributions using the command `wsl -l -v`
* Then open the desired distribution with the command `wsl -d <distroName>`, where "distroName" is the name of the installed Linux distribution

## Access Windows drives in WSL
 * Open a Linux distribution in command line
 * The Windows operating system drives can be accessed inside the WSL Linux distributions using the `/mnt` path. For example running the command `cd /mnt/c` will change the working directory to C drive.

## Access WSL files from windows file explorer
* Open  windows file explorer
* In the left pane, a section named `linux` will be visible. Click on it to see the folders of the installed WSL Linux distributions in Windows file explorer

## Run Linux commands in windows with 'wsl' prefix
* Linux commands can be run in windows command line by just adding the 'wsl' prefix
* For example, we can run the command `wsl ls -l` to list the files and folders in windows command prompt.
* Using the pipe operator (`|`), we can combine both Linux and windows commands to pass output of one command to another. For example, the command `dir | wsl grep "xyz"` will pass the output of windows command `dir` to Linux command `grep`

## Shutdown Linux distributions
* Run the command `wsl --shutdown` to shutdown all the installed Linux distributions
* Run the command `wsl -t <distroName>` to shutdown only a single installed Linux distribution. The installed "distroName" can be obtained by running the command `wsl -l`

## Update WSL
* WSL kernel can be updated from command line using the command `wsl --update` . However by WSL will update automatically with windows update 

## Update a WSL Linux distribution
* Open the desired Linux distribution from start menu or with the `wsl` command
* If a Debian based Linux distribution like Ubuntu is installed, then it can be updated using the command `sudo apt update && sudo apt upgrade` 
* Now the packages in the Linux distribution will be updated

## Uninstall a Linux distribution
* First view the list of installed Linux distributions using the command `wsl -l -v`
* Then run the command `wsl --unregister <distroName>` where "distroName" is the name of the Linux distribution to be uninstalled
* Alternatively, a Linux distribution can also be manually uninstalled from "Add or remove programs" section in the System Settings

### Video
The video for this post can be found [here](https://youtu.be/xxQer-OyAD4)

<iframe width="560" height="315" src="https://www.youtube.com/embed/xxQer-OyAD4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
 
### References
* Basic wsl commands reference - https://learn.microsoft.com/en-us/windows/wsl/basic-commands#install
* Install wsl from command line - https://learn.microsoft.com/en-us/windows/wsl/install
* wsl manual installation for older windows versions - https://learn.microsoft.com/en-us/windows/wsl/install-manual
* A post on useful wsl commands - https://adamtheautomator.com/windows-subsystem-for-linux/#Setting_WSL_Configuration_Items_at_Bootup_with_wslconf 

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg0OTkwMDE1MV19
-->