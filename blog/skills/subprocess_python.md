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
* Write functions in other languages like Java, Dotnet etc., create an executable file and communicate with command line inputs and outputs. This use case occurs when there is some legacy module, or if there is an API for a system in non-python language.

## How it works
* `subprocess` module can run child processes, communicate with them over their input / output / error pipes (command line outputs and inputs)
* Return code can also be obtained after running the child process to get the status of execution

### Example 1 - Run external commands
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
proc = Popen(commandWords, stdout=PIPE, stderr=PIPE)

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
* As shown in the above example, inputs can be provided to a command or an external program via command line arguments, and command line output can be used to fetch the execution results by our python program
* Any errors thrown by the external command can be captured in the variable `errs`
* The above example is applicable for running external programs also instead of OS commands
	* For example there is and exe file called "hello.exe" that takes a named command line input called `--name` and outputs the greeting
	* python can interact with it using `commandWords = ["hello.exe", "--name", "James"]` and the output string would be "Hello James !!!"

## Example-2 "cwd" option to change the directory of command execution
```py
from subprocess import Popen, PIPE

command = "hello.bat James"
commandFolder = "batFolder/"

# create a child process object
# to run a batch file, shell=True to be added additionally
proc = Popen(command.split(" "), stdout=PIPE, stderr=PIPE, cwd=commandFolder, shell=True)

# run the child process and capture the output and errors
try:
    outs, errs = proc.communicate()
except:
    proc.kill()
    quit()

# derive the command line response strings
resp = outs.decode("utf-8")
errStr = errs.decode("utf-8")

# print the response string
print("Response*************************")
print(resp)
print("Errors*************************")
print(errStr)
```

### Example 2 - Communicate with other languages over command line
* `subprocess` can be used to interact with other languages running the those programs and interact with them over command line
```py
# importing from 'subprocess' python module
from subprocess import Popen, PIPE

def computeFromExternal(num1, num2):
    commandFolderPath = "compute/"

    command = f"dotnet run {num1} {num2}"

    # create a child process object
    proc = Popen(command.split(" "), stdout=PIPE, stderr=PIPE, cwd=commandFolderPath)

    # run the child process and capture the output and errors
    try:
        outs, errs = proc.communicate()
    except:
        proc.kill()
        return "Error thrown while subprocess execution..."

    # errors thrown by the code
    errStr = errs.decode("utf-8")
    # derive the command line response string
    resp = outs.decode("utf-8")

    # print("Output*************************")
    # print(resp)
    # print("Errors*************************")
    # print(errStr)
    # print("*************************")

    # check for errors thrown by code
    if not len(errStr) == 0:
        return "Error thrown by the code..."

    # extract the subprocess result
    reslt = float(resp.strip())

    return f"The computation result is {reslt}"


print(computeFromExternal(5.1, 3.2))
print(computeFromExternal("abcd", 3.2))
```

* In the above python code a function named  `computeFromExternal` runs a dotnet project present in a folder named `compute/` present in the same folder as the python code
*  The inputs to the dotnet code are provided via command line arguments.
* The outputs and error strings are parsed from the variables `outs` and `errs` respectively   


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
eyJoaXN0b3J5IjpbNjI4NTc3NTUwLDIxNDkwMzU1Nyw3ODAzMz
I1NCwxMjA2NjY0NjEwLC01MDM0MTA0MTMsLTE1MTkxMjc4NDYs
MTUzNDU3MjA0NCwxMDMxMzczODA1LDk4NTAzMjA4MiwtMTE5OD
A2MjU0MCwtODM3NzczNDc4LC00OTg5ODg1OTgsMTgwMDY3MzQ2
MywtMjA1NzQ5NTQ1OCwxNDQ2MjU3MTU3LDEzMzg5Mjk2NTAsMz
EwMjg2Mzc0XX0=
-->