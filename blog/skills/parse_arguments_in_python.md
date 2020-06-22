## Skill - parse command line arguments in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will understand how to read command line arguments using `argparse` module

Install **argparse** module by entering the following in command prompt
```
pip install argparse
```

We can take named inputs from command line using `argparse` module
Suppose we want to read a named argument say name, then user should type `--name <username>`
Suppose we want to read multiple named arguments say firstName and lastName, then user should type `--firstName <firstName> --lastName <lastName>`


#### Example
Create a new file named `hello.py` with the following code
```python
# hello.py
import argparse
parser = argparse.ArgumentParser()

# add argument with flag --name
parser.add_argument('--name', help='Persons name')
args = parser.parse_args()

# read name from arguments
name = args.name

if name!=None:
    print('Hello {0} !!!'.format(name))
else:
    print('name not provided...')
```
If you run `hello.py --name Sudhir` then you should see `Hello Sudhir !!!` in the output


### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://www.tutorialspoint.com/execute_python_online.php

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/UnfitUnsteadyExpertise?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### References
* Official tutorial - https://docs.python.org/3/library/argparse.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU5ODA1Mjc5NV19
-->