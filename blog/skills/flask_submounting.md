## Skill - Sub mounting a flask application under a URL prefix

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to sub-mount a flask application under a URL prefix

## Use cases
Mounting an application under a URL prefix can help in 
* dispatching multiple flask applications from a single server
* Placing the flask application behind a reverse proxy like (nginx or IIS) with a URL prefix. URL prefix is required because the reverse proxy can serve multiple applications each with different URL prefix

![reverse_proxy_arch image](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/reverse_proxy_arch.png)
## Sub mounting an application using DispatcherMiddleware class  
* DispatcherMiddleware class can be used to dispatch one or more flask applications each with different URL prefix
* Each URL prefix should start with a `/` (example `/app1`)
* If no prefixes are matched, the DispatcherMiddleware can be configured to route the requests to a particular flask application or send a "404 not found" error  

### Example
```py
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
* In the above example, the flask application named `app` is sub-mounted under a URL prefix "/myApp"
* In case of no matching URL prefix, "404 not found page" will be returned

### Multiple flask apps example
```py
from flask import Flask
from werkzeug.middleware.dispatcher import DispatcherMiddleware
from werkzeug.exceptions import NotFound

app1 = Flask(__name__)

@app1.route('/')
def index1():
    return "App1 Hello World!!!"

@app1.route('/help')
def helpPage1():
    return "App1 Help Page"

app2 = Flask(__name__)

@app2.route('/')
def index2():
    return "App2 Home Page"

@app2.route('/help')
def helpPage2():
    return "App2 Help Page"


app3 = Flask(__name__)

@app3.route('/')
def index3():
    return "App3 Home"

@app3.route('/help')
def helpPage3():
    return "App3 Help Page"

hostedApp = Flask(__name__)
hostedApp.wsgi_app = DispatcherMiddleware(app1, {
    "/abc": app2,
    "/def": app3
})

# run the server
hostedApp.run(host="0.0.0.0", port=50100, debug=True)
```
* In the above example, 3 different flask applications are dispatched from a single server using DispatcherMiddleware
* DispatcherMiddleware is configure to route the requests to `app1` if no URL prefixes are matched
* The requests are sent to `app2` if the URL prefix is "abc" and the  requests are sent to `app3` if the URL prefix is "def"

### References
* DispatcherMiddleware docs - https://flask.palletsprojects.com/en/2.2.x/patterns/appdispatch/#combining-applications


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMjE2MDIxNDIsLTc2MjIxNTI0MiwtMT
IxNTk4Mjc2OCwtMTU4MjEzNTc2NiwtMjA4ODc0NjYxMl19
-->