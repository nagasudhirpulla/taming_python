## Skill - Run external commands or communicate with other languages using python subprocess module
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)

Please go through the above skills if necessary for reference or revision
<hr/>

* In this post we will understand how run external commands or call other languages in python using the `subprocess` module
* `subprocess` module generally comes included with python installation. So no need to install the module separately.

## Use Cases 
* Run OS commands or call external programs from python (like "ping google.com", "ipconfig" etc) over command line inputs and outputs
* Write functions in other languages like Java, Dotnet etc., create an executable file and communicate with command line inputs and outputs

## How it works
* `subprocess` module can run child processes, communicate with them over their input / output / error pipes (command line outputs and inputs)
* Return code can also be obtained after running the child process to get the status of execution

### Example - Run external commands
* The following example  
	* runs the command "ping google.com"
	* captures the command line output and prints it
	* applies custom logic on the execution results via command line output

```python
# importing from 'subprocess' python module
from subprocess import Popen, PIPE

# inputs can be provided in the form of additional arguments
# for example, execute a command 'ping google.com -n 2' using ["ping", "google.com", "-n", "2"]
commandWords = ["ping", "google.com"]

# create a child process object
proc = Popen(commandWords, stdout=PIPE)

# run the child process and capture the output and errors
try:
    outs, errs = proc.communicate()
except:
    proc.kill()
    quit()

# derive the command line response string
resp = outs.decode("utf-8")

# print the response string
print("*************************")
print(resp)
print("*************************")

# apply some logic on the response 
if "Lost = 0 (0% loss)" in resp:
    print("Perfect ping!!!")
else:
    print("Not a perfect ping...")
```


### Video
Video for this post can be found [here](https://youtu.be/nsVkTslyBcE)

<iframe width="560" height="315" src="https://www.youtube.com/embed/nsVkTslyBcE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### References
* Official docs - https://docs.python.org/3/library/subprocess.html
* https://github.com/nagasudhirpulla/pmu_report_generator/blob/master/src/services/pmuDataFetcher.py
* https://eli.thegreenplace.net/2017/interacting-with-a-long-running-child-process-in-python/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcxOTk0MDcwLDE4MDA2NzM0NjMsLTIwNT
c0OTU0NTgsMTQ0NjI1NzE1NywxMzM4OTI5NjUwLDMxMDI4NjM3
NF19
-->