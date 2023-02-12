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
* In the above command, `--no-index` specifies to ignore the pypi package index for fetching the packages for installation
* In the above command, the `-f` flag is used to specify the folder path to fetch and install the python package

### Video
You can see the video on this post [here](https://youtu.be/5tYM5awtxek) 

<iframe width="560" height="315" src="https://www.youtube.com/embed/5tYM5awtxek" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

### References
* https://packaging.python.org/en/latest/tutorials/installing-packages/#installing-from-local-archives

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIyMzg0Njc2MiwzMjUxMzEwMjQsLTk2Nz
kyMzUzOSw2NTIwODA3NjQsLTgxNzY2MTgzNywtMTU5MDk4NTk4
NiwtODcwOTI0MDgwLC0yMDg4NzQ2NjEyXX0=
-->