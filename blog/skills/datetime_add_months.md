## Skill - Add or subtract months to date in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Python datetime library](https://nagasudhir.blogspot.com/2020/05/datetime-library-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

`datetime` module in python is very useful in manipulating date-times.
`calendar` module in python is very useful in performing general calendar related functions
<hr/>
In this post we will learn how to add months to a datetime in python

Let number of months to add to a particular datetime be k

The algorithm we are using is as follows

* Add a input floored month - 1 + k to input year to get result year component
* Result month component would be (input month -1 + k)%12 + 1
* Result day component would be minimum of input date component and max date of that result month (For example we cant have day co)


### Online Interpreter
You can run these codes online at https://www.programiz.com/python-programming/online-compiler/ or https://repl.it/

### You can practice here


<hr/>

### References
* Official documentation - https://docs.python.org/3/library/calendar.html

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEFkZCBvciBzdWJ0cmFjdC
Btb250aHMgdG8gZGF0ZSBpbiBweXRob25cbmF1dGhvcjogTmFn
YXN1ZGhpciBQdWxsYVxuZGF0ZTogJzIwMjAtMDYtMjYnXG4iLC
JoaXN0b3J5IjpbLTEwMDA0OTgyMjgsMTA2ODM0MTAwMCw3MzA5
OTgxMTZdfQ==
-->