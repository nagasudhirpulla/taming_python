## Skill - Setup python on Linux in Windows using WSL and VS Code

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>

In this post we will learn
* Set up python in Ubuntu inside WSL
* Setup multiple python versions using deadsnakes ppa
* Run python and install packages in WSL (Windows Subsystem for Linux)
* Visual Studio Code (VS Code) support for WSL
* Set up virtual environments for python projects
* `update-alternatives` command for aliasing python version with `python` command 

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
 

## Setup multiple python versions using deadsnakes ppa
* deadsnakes ppa contains multiple versions of python that can be installed and used in Ubuntu
* Add deadsnakes ppa repository using `sudo add-apt-repository ppa:deadsnakes/ppa`
* Now multiple python versions can be installed. For example python 3.7 and python 3.9 can be installed using the following commands
```bash
# install python 3.7
sudo apt install python3.7
sudo apt install python3.7-distutils
# install python 3.9
sudo apt install python3.9
sudo apt install python3.9-distutils
```
* After installation, multiple python versions can be used. For example `python3.9 --version` command will use python 3.9 and `python3.7 --version` will use python 3.7

## Run python and install packages in WSL
* Suppose there is a python script named `hello.py`
* It can be run with python installed in WSL using the command  `wsl python3 hello.py`
* To run with another version of python, say python 3.7, we can use the command `wsl python3.7 hello.py`
* External packages can be installed using `pip`. For example `python3 -m pip install flask` will install the flask python module. 
* External packages can be installed in other python environments also using `pip`. For example `python3.9 -m pip install flask` will install flask in python 3.9 environment.

### Run flask server in WSL
* For example, a server in `server.py` file can be run using the command `wsl python3 server.py`
* The server page can be accessed in windows browser without opening WSL

## VS Code support for WSL
* Visual Studio Code supports easy interface for running python from WSL with `WSL` VS Code extension
* After installing WSL, open command palette with Ctrl+Shift+P shortcut and type WSL. Select "WSL: Open Folder in WSL".
* Now a folder in VS Code will be opened from an installed WSL distribution
* Python extension should again be installed in VS Code for WSL to enable VS Code python support for folders opened in WSL 
* Python version and virtual environment can be selected easily using the options present in the status bar at the bottom of VS Code editor
 
### References
* WSL VS Code extension - https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5ODQ4MzgwNzQsLTE4MTExMDI0NzMsMT
k0MTUyNDU2NSwtMTc1MzQyODM2NiwtMTE2OTEzMjYyNl19
-->