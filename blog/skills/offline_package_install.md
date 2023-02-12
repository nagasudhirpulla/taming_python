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
*  

### Step 1 - Download the python package along with dependencies into a folder  
* Open command prompt
* Use command `pip install <package_name>`
* For example, to install a package named pandas, you need to run 
`pip install pandas`

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
eyJoaXN0b3J5IjpbMTc4ODg3MTM4NCwtMTU5MDk4NTk4NiwtOD
cwOTI0MDgwLC0yMDg4NzQ2NjEyXX0=
-->