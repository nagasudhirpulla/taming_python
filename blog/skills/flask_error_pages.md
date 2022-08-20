## Skill - Custom Error Pages in python Flask application

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Serve static files in flask](https://nagasudhir.blogspot.com/2022/04/serve-static-files-in-flask.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to create custom error pages in a flask application and simulate errors in flask application

## Use cases
We can serve custom error pages for
* Providing additional content in the error pages like links to other pages etc
*  


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

### Combining multiple flask applications
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

### Video
The video for this post can be seen [here](https://youtu.be/_JiJGFAW43s)

<iframe width="560" height="315" src="https://www.youtube.com/embed/_JiJGFAW43s" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* DispatcherMiddleware docs - https://flask.palletsprojects.com/en/2.2.x/patterns/appdispatch/#combining-applications


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQxMTEyMTIyM119
-->