## Skill - Install and manage python packages
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

### Install a python package
* Open command prompt
* Use command `pip install <package_name>`
* For example, to install a package named pandas, you need to run 
`pip install pandas`

### Install specific version of a python package
* Open command prompt
* Use command `pip install <package_name>==<version_number>`
* For example, to install a package named numpy with version 1.11.1, you need to run 
`pip install numpy==1.11.1`

### restore / install packages from a file using '-r' flag
* If we have a text file named `requirements.txt` with packages information as shown below
```
MySQL-python==1.2.3
WebOb==1.2.3
numpy==1.11.1
```
* We can install all the packages from the file like the one file shown above using the

### Further Reading
* https://www.shellhacks.com/pip-install-specific-version-of-package/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEluc3RhbGwgYW5kIG1hbm
FnZSBwYWNrYWdlcyBpbiBweXRob25cbmF1dGhvcjogTmFnYXN1
ZGhpciBQdWxsYVxuZGF0ZTogJzIwMjAtMDUtMjUnXG50YWdzOi
AncHl0aG9uLCBsZWFybmluZywgdHV0b3JpYWwsIHRhbWluZ19w
eXRob25fc2tpbGwnXG5jYXRlZ29yaWVzOiB0YW1pbmdfcHl0aG
9uX3NraWxsXG4iLCJoaXN0b3J5IjpbLTM2MDcwODgwMywxNDEy
NzYwMDU0LDIxMDM5MDI0MSw3MzA5OTgxMTZdfQ==
-->