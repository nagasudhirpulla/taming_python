## Skill - IIS as a reverse proxy for python flask application

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Sub mounting a flask application under a URL prefix](https://nagasudhir.blogspot.com/2022/08/sub-mounting-flask-application-under.html)
* [Run a python Flask server as a windows background service using nssm](https://nagasudhir.blogspot.com/2022/09/run-python-flask-server-as-windows.html)
* [Waitress as Flask server WSGI](https://nagasudhir.blogspot.com/2022/10/waitress-as-flask-server-wsgi.html)


Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to run a flask server behind IIS acting as a reverse proxy for the flask application

## What is IIS
* Internet Information Services (IIS) is a general purpose web server in windows for hosting web applications
* It is a production ready web server with good security, stability and many configuration options

## Why use IIS as reverse proxy
- Hosting a python flask server directly to the internet is not generally practiced  
- Flask server should be generally hosted behind a robust reverse proxy server like Nginx or IIS (Internet Information Services)
- SSL certificate management will be very easy with IIS and need not be handled in the flask application
- Since IIS is the go to hosting solution for windows server, this approach is a more useful and a practical implementation of flask server hosting  in windows  
- Moreover IIS has a very handy and powerful user interface to control the hosting of web applications

### Enabling IIS in windows
-   In windows search for “Turn Windows features On or Off”
-   Under the “Internet Information Services” section, make sure that “IIS Management Console” and default options under "World Wide Web Services" are enabled

## Architecture
* The data flow to the flask application can be as shown below
* The flask application can be a windows background service or a normal process running in command prompt.
![flask_IIS_reverse_proxy_arch.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/flask_IIS_reverse_proxy_arch.png)
## Example Flask server
* Let us create a simple flask server for this example
* Create a `server.py` file that acts as a flask server
```py
# server.py  
from flask import Flask
from werkzeug.middleware.dispatcher import DispatcherMiddleware
from werkzeug.exceptions import NotFound

# create a server instance
app = Flask(__name__)

@app.route('/')
def index():
    return "Hello World!!!"

@app.route('/help')
def helpPage():
    return "This is the Help Page"

hostedApp = Flask(__name__)
hostedApp.wsgi_app = DispatcherMiddleware(NotFound(), {
    "/myApp": app
})

# run the server
hostedApp.run(host="0.0.0.0", port=50100, debug=True)
```
* Notice that the flask application is sub-mounted under the URL prefix '/myapp' . Visit [this blog post](https://nagasudhir.blogspot.com/2022/08/sub-mounting-flask-application-under.html) to understand more on how to sub-mount a flask application under a URL-prefix 
* Also consider using waitress for running the application in production. Visit [this blog post](https://nagasudhir.blogspot.com/2022/10/waitress-as-flask-server-wsgi.html) to understand how to use waitress as WSGI for a flask application

### Running the flask server
* You can run the flask server in command line using the command `python server.py`
* You can also use nssm to run the flask server as a windows background service. Read [this blog post](https://nagasudhir.blogspot.com/2022/09/run-python-flask-server-as-windows.html) for more information on this

## Setting up IIS as reverse proxy

### Step 1 - Installing the url-rewrite and ARR modules in IIS
* url-rewrite module of IIS can be downloaded and installed from from https://www.iis.net/downloads/microsoft/url-rewrite . Web platform installer in IIS can also be used to install url-rewrite module in IIS
* ARR (Application Request Routing) module can be downloaded and installed in IIS from https://www.iis.net/downloads/microsoft/application-request-routing . Web platform installer in IIS can also be used to install ARR module in IIS
* url-rewrite and ARR modules are required in IIS to serve as a reverse proxy for a flask application

### Step 2 - Enable Proxy in ARR module
- Open IIS Manager and click on the server  
- In  the admin console for the server, double click on the Application Request Routing option:  
- Click  the Server Proxy Settings action on the right-hand pane
- Select  the Enable proxy checkbox so that it is enabled
- Click  Apply and proceed with the URL Rewriting configuration

### Step 3 - URL rewriting
- Double click URL rewrite icon in Default Website  
- Click Add Rule(s) link in the right pane  
- Select Blank rule under Inbound rules

### Step 4 (Optional)  -  Allow  HTTP_X_ORIGINAL_HOST server variable
Using a reverse proxy will modify the request headers originating from the end-user's browser. Hence the HTTP header `host` will not be known to the flask application. So using the below steps we can send a new HTTP header named `HTTP_X_ORIGINAL_HOST` to send original host header to flask application  
- Double click URL rewrite icon in Default  Website  
- Click on View Server Variables in the right-hand pane  
- Add  HTTP_X_ORIGINAL_HOST to the allowed server variables

### Install nssm in windows
* Download nssm zip file from https://nssm.cc/download and unzip into a folder in C drive
* In the 'Path' system environment variable, add the path of nssm.exe, so that nssm.exe can be recognized in command line


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
eyJoaXN0b3J5IjpbLTI2MzIwNTMzMCwxNTM1NjQ4NjIzLDU2ND
Y0OTY0NiwtODgwNDE1NDkyXX0=
-->