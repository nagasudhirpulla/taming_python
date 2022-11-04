## Skill - Run external commands or other languages using python subprocess module
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)

Please go through the above skills if necessary for reference or revision
<hr/>

* In this post we will understand how run external commands or call other languages in python using the `subprocess` module
* `subprocess` module generally comes included with python installation. So no need to install the module separately.

## Use Cases 
* Running OS commands from python (like "ping google.com", "ipconfig" etc)
* Communicate with other languages over command line from python
* 



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
* https://github.com/nagasudhirpulla/pmu_report_generator/blob/master/src/services/pmuDataFetcher.py
* https://eli.thegreenplace.net/2017/interacting-with-a-long-running-child-process-in-python/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbNDMyNDA2NTgsMzEwMjg2Mzc0XX0=
-->