## Skill - Run flask application over HTTPS

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to run a flask application over HTTPS 

## "adhoc" option for testing purposes
```py
from flask import Flask

# create a server instance
app = Flask(__name__)

@app.route('/')
def index():
    return "Hello World!!!"

# run the server
app.run(host="0.0.0.0", port=50100, debug=True, ssl_context="adhoc")
```

* As shown in the above code, add an input `ssl_context="adhoc"` in the `app.run` function. 
* This will run the flask application over HTTPS with a dummy SSL certificate
* This method is very easy and useful for development purposes
 

## Why use IIS as reverse proxy
- Hosting a python flask server directly to the clients / internet is not generally practiced  
- Flask server should be generally hosted behind a robust reverse proxy server like Nginx or IIS (Internet Information Services)
- SSL certificate management will be very easy with IIS and need not be handled in the flask application
- Since IIS is the go-to hosting solution for windows server, this approach is a more useful and a practical implementation of flask server hosting  in windows  
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
This url-rewrite rule forwards the request from IIS to the flask application hosted at localhost:50100 if the request URL starts with '/myapp'

- Double click URL rewrite icon in Default Website  
- Click Add Rule(s) link in the right pane  
- Select Blank rule under Inbound rules
- Create a rule as shown in the image below

![flask_iis_url_rewrite.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/flask_iis_url_rewrite.png)
- Server variables section in the above settings should not be set if Step 4 is not done

### Step 4 (Optional)  -  Add HTTP_X_ORIGINAL_HOST server variable
Using a reverse proxy will modify the request headers originating from the end-user's browser. Hence the HTTP header `host` will not be known to the flask application. So using the below steps we can send a new HTTP header named `HTTP_X_ORIGINAL_HOST` to send original host header to flask application from the end user
- Double click URL rewrite icon in Default  Website  
- Click on View Server Variables in the right-hand pane  
- Add  HTTP_X_ORIGINAL_HOST to the allowed server variables

## Conclusion
* By following the above steps, IIS can be used as a reverse proxy for the flask application

### Video
The video for this post can be seen [here](https://youtu.be/6_Hpug3l2I0)

<iframe width="560" height="315" src="https://www.youtube.com/embed/6_Hpug3l2I0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## References
* Flask quickstart guide - https://flask.palletsprojects.com/en/2.2.x/quickstart/
* 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjExMDg2OTQsNDk5MDkzMTYyLDgxMTkyNj
AxNCw0MTAwMzI4OF19
-->