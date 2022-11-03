## Skill - Run other languages or external programs from python using subprocess module
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

* Suppose we want to read a named argument say name, then user should type `--name <name>`
* Suppose we want to read multiple named arguments say firstName and lastName, then user should type `--firstName <firstName> --lastName <lastName>`

If named argument is not provided, then argparse will return `None`

### Example
Create a new file named `hello.py` with the following code
```python
# import argparse module and get parser
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

### Video
Video for this post can be found [here](https://youtu.be/nsVkTslyBcE)

<iframe width="560" height="315" src="https://www.youtube.com/embed/nsVkTslyBcE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### References
* Official tutorial - https://docs.python.org/3/library/argparse.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU2NDM3NjkyOV19
-->