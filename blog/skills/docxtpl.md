## Skill - python docxtpl for automating reports and invitations
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision



```python
import pandas as pd
# create a dataframe
x = {
	"Name": ["Harris", "Miss. Elizabeth"],
	"Age": [22, 58],
	"Sex": ["male", "female"]
	}
df = pd.DataFrame(x)

print(df.shape)
# this will print (2,3)

print('Number of rows = {0}'.format(df.shape[0]))
print('Number of columns = {0}'.format(df.shape[1]))
'''
this will print
Number of rows = 2
Number of columns = 3
'''
```
### Video
Video for this post can be found [here](https://youtu.be/xVPX-Y7f-eE)

<iframe width="560" height="315" src="https://www.youtube.com/embed/xVPX-Y7f-eE" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### References
* Official tutorial - https://pandas.pydata.org/pandas-docs/stable/getting_started/index.html
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg1ODcyMDg2XX0=
-->