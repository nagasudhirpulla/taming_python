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
* Write functions in other languages like Java, Dotnet etc., create an executable file and communicate with command line inputs and outputs. This use case occurs when there is some legacy module, or if there is an API for a system in non-python language, or you don't want to re-write existing non-python modules in python

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
# shell=True to be added to run batch files, otherwise not required
proc = Popen(command.split(" "), stdout=PIPE, stderr=PIPE, cwd=commandFolder, shell=True)

# run child process and capture the output and errors
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
* In the above example, there is a batch file located in the folder location `batFolder/` relative to the python script
* 'cwd' option is used to change the command execution directory in the `Popen` constructor call
* This way, using `cwd` option, we can run programs present in other folders also

### Example 3 - Communicate with other languages over command line
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

* In the above python code a function named  `computeFromExternal` runs a dotnet project program in the folder `compute/` relative to the python code (absolute folder paths can also be used if required)
*  The inputs to the dotnet code are provided via command line arguments
* The outputs and error strings are parsed after command execution from the variables `outs` and `errs` respectively

### Better way to run other language code
* Running other language code via command line requires the language runtime to be present in the system. For example, the previous example requires dotnet and some dotnet packages to be installed in the machine running the python code.
* To eliminate the dependency of other language runtime, the external code can be packaged into a self-contained exe file and that can be used by the python code. This makes the other language code portable and removes the requirement of installing other language runtime.

<hr/>

### References
* Official docs - https://docs.python.org/3/library/subprocess.html
* https://github.com/nagasudhirpulla/pmu_report_generator/blob/master/src/services/pmuDataFetcher.py
* https://eli.thegreenplace.net/2017/interacting-with-a-long-running-child-process-in-python/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA1NjY4NTU0MywtNjI1ODE1NTI2LDIxND
kwMzU1Nyw3ODAzMzI1NCwxMjA2NjY0NjEwLC01MDM0MTA0MTMs
LTE1MTkxMjc4NDYsMTUzNDU3MjA0NCwxMDMxMzczODA1LDk4NT
AzMjA4MiwtMTE5ODA2MjU0MCwtODM3NzczNDc4LC00OTg5ODg1
OTgsMTgwMDY3MzQ2MywtMjA1NzQ5NTQ1OCwxNDQ2MjU3MTU3LD
EzMzg5Mjk2NTAsMzEwMjg2Mzc0XX0=
-->