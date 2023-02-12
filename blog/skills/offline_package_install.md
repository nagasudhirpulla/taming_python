## Skill - Install python packages offline without internet

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Install and manage python packages](https://nagasudhir.blogspot.com/2020/05/install-and-manage-packages-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will learn how to use install python packages offline from files without internet

### Use cases
Offline installation of python packages can be useful in the following scenarios
* Installing python packages in a computer that has no access to internet
* Installing python packages from files in multiple computers to save internet bandwidth

### Step 1 - Download the python package along with dependencies into a folder  
* In a computer that has internet access, create an empty folder where the required python packages will be downloaded. Let the path of the folder be `C:\Users\Abcd\offline_packages\packages_folder`
* Let us download a python package named `flask` into the folder
* In a command prompt type the following command. The python package along with it's dependencies will be downloaded into the folder
```bash
pip download -d "C:\Users\Abcd\offline_packages\packages_folder" flask
```
* In the above command, the directory location is specified using the `-d` flag

### Step 2 - Install the package in the computer without internet
* Copy the folder containing the package files downloaded in step 1 into the computer without internet. Let the folder path be `C:\Users\Xyz\packages_folder`
*  Install the package from the folder using the following command
```bash
pip install --no-index -f "C:\Users\Xyz\packages_folder" flask
```
* Now the python package is installed from package files inside the folder. You can verify the installed packages using the command `pip list`
* In the above command, `--no-index` specifies not to ignore the pypi package index for fetching the packages for installation
* In the above command, `-f` is used to specify the folder path to fetch and install the python package 

### Install specific version of a python package
* Open command prompt
* Use command `pip install <package_name>==<version_number>`
* For example, to install a package named numpy with version 1.11.1, you need to run 
`pip install numpy==1.11.1`

### list all the packages in a python environment
* Open command prompt
* Use command `pip list`
* All the installed python packages along with their version numbers will be displayed

### install packages from a file using '-r' flag
* If we have a text file named `requirements.txt` with packages information as shown below
```
MySQL-python==1.2.3
WebOb==1.2.3
numpy==1.11.1
```
* We can install all the packages from the file like the one file shown above using the following command
`pip install -r requirements.txt`
* To install packages from a file located at a specific path, use a command something like the one below
`pip install -r C:\Users\Nagasudhir\Documents\requirements.txt`

### dump all the packages information into a text file
* In order to dump the installed packages information of the current python environment use the following command
`pip freeze > requirements.txt`

### Further Reading
* https://www.shellhacks.com/pip-install-specific-version-of-package/

### Video
The video for this post can be seen [here](https://youtu.be/3eItCqPqGF8)

<iframe width="560" height="315" src="https://www.youtube.com/embed/3eItCqPqGF8" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcwNzA3MTQyMSwtOTY3OTIzNTM5LDY1Mj
A4MDc2NCwtODE3NjYxODM3LC0xNTkwOTg1OTg2LC04NzA5MjQw
ODAsLTIwODg3NDY2MTJdfQ==
-->