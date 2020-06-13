## Skill - Install a python package from source code

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Install and manage python packages](https://nagasudhir.blogspot.com/2020/05/install-and-manage-packages-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will learn how to install python packages from source code. This scenario can occur where the computer does not have internet access.

### Steps to install package from source code
* Download or copy the source code to a folder. For example the source code folder may be like `C:\Users\Nagasudhir\Downloads\mypackage`
* open command prompt
* run cd command to make the source code folder as the working directory. For example `cd C:\Users\Nagasudhir\Downloads\mypackage`
* run the command `python setup.py install`

Please note that the above method works for most of the cases. Sometimes the creator of the package will give specific instructions in the GitHub page on how to install the package from source.

In most of the cases, the package may require some other packages to be installed as dependencies. Make sure those dependencies are installed before installing from source code.


### Further Reading
* official documentation - https://pip.pypa.io/en/stable/reference/pip_install/#examples

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwODY1MTY0ODAsMTAwMjM2NDUxM119
-->