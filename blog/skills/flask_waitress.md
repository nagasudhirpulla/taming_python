## Skill - Run a python Flask server with waitress as WSGI

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)


Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to use waitress as a WS for a flask application

## What is nssm
* nssm runs commands or batch files (in our case, the flask application) as background services in windows
* The services are also restarted in case of failure
* The services can be easily managed using services.msc in windows
* Command line output can be saved in log files as text
* The generated logs can also be rotated based on time and log file size criteria
* nssm also has a graphical editor to manage it's services

### Install nssm in windows
* Download nssm zip file from https://nssm.cc/download and unzip into a folder in C drive
* In the 'Path' system environment variable, add the path of nssm.exe, so that nssm.exe can be recognized in command line

## Example Flask server
The following is an example flask server that we will run as a background service in windows
```py
from flask import Flask
app = Flask(__name__)

@app.route('/')
def index():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=50100, debug=True)
```

### Step 1 : Create a batch file to run the server
* Create a batch file say `run_server.bat` that will run the python server in a command line. You can check by running the batch file. Keep the batch file in the same folder as the 'server.py' file.
```bat
call python server.py
```

### Step 2 : Use nssm to run the batch file as a background service
* Open a command prompt as an administrator. Change the directory of the command prompt to the directory where the 'run_server.bat' is present using 'cd' command.
* Run the following commands to run the batch file as a background service
```bat
call nssm.exe install my_flask_app "%cd%\run_server.bat"
call nssm.exe set my_flask_app AppStdout "%cd%\logs\my_flask_app_logs.log"
call nssm.exe set my_flask_app AppStderr "%cd%\logs\my_flask_app_logs.log"
call nssm set my_flask_app AppRotateFiles 1
call nssm set my_flask_app AppRotateOnline 1
call nssm set my_flask_app AppRotateSeconds 86400
call nssm set my_flask_app AppRotateBytes 1048576
call sc start my_flask_app
```
The commands are explained as shown below
* `nssm.exe install my_flask_app "%cd%\run_server.bat"` will register a background service named "my_flask_app" and that runs the command `"%cd%\run_server.bat"`. Here `%cd%` means the 'current directory'
* The below commands will set the file paths to log the output and error streams of command line.
```bat
nssm.exe set my_flask_app AppStdout "%cd%\logs\mis_dashboard.log"
nssm.exe set my_flask_app AppStderr "%cd%\logs\mis_dashboard.log"
```
Ensure there is a folder named 'logs' in the folder containing 'server.py' file.
* `nssm set my_flask_app AppRotateFiles 1` will enable log rotation
* `nssm set my_flask_app AppRotateOnline 1` will rotate log files even if application is running
* `nssm set my_flask_app AppRotateSeconds 86400` will rotate log files after 86400 seconds (1 day)
* `nssm set my_flask_app AppRotateBytes 1048576` will rotate log files after log files reaches 1048576 bytes (1 MB) size
* `sc start my_flask_app` will start the background service

![nssm_install_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/nssm_install_demo.png)

### Edit the service using nssm GUI
```bat
nssm edit my_flask_app
```

![nssm_edit_service_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/nssm_edit_service_demo.png)

## Manage windows background services
* Open Services app or run "services.msc" to open the services app in windows
* The service can be started and stopped in this application

![nssm_services_msc_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/nssm_services_msc_demo.png)

### 'sc' command to manage services in command line
* Delete a service - `sc delete my_flask_app`
* Start a service - `sc start my_flask_app` 
* Pause a service - `sc pause my_flask_app`
* Stop a service - `sc stop my_flask_app`

### View status of a service in command line
`sc query my_flask_app`

![sc_query_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/sc_query_demo.png)
### Video
The video for this post can be seen [here](https://youtu.be/oKciAtJTuSw)

<iframe width="560" height="315" src="https://www.youtube.com/embed/oKciAtJTuSw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## References
* nssm usage guide - https://nssm.cc/usage
* nssm download link - https://nssm.cc/download
* Flask quickstart guide - https://flask.palletsprojects.com/en/2.2.x/quickstart/

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNDI4Mjg5NzksNzg4Nzg5MzAzXX0=
-->