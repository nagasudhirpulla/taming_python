## Skill - PyInstaller
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)


Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

In this post, we will learn how to distribute our python program as an `exe` file

The shape attribute returns the shape of DataFrame as  (nRows, nColumns)
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

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/DaringFastUser?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### References
* Official tutorial - https://pandas.pydata.org/pandas-docs/stable/getting_started/index.html
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFVzaW5nIFB5SW5zdGFsbG
VyIGZvciBkaXN0cmlidXRpbmcgcHl0aG9uIHByb2dyYW1cbmF1
dGhvcjogTmFnYXN1ZGhpciBQdWxsYVxuZGF0ZTogJzIwMjAtMD
YtMTgnXG4iLCJoaXN0b3J5IjpbNjQxODQ5NzU0XX0=
-->