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
    "/app": app
})

# run the server
hostedApp.run(host="0.0.0.0", port=50100, debug=True)
```
* int, float, path, uuid are the supported variable types that can be extracted from URL segments

### extract variables from URL query parameters
* using request.args imported from flask module, we can extract the query parameters from URL
* using request.args.to_dict() function, we can get the URL query parameters as a python dict object
```py
from flask import Flask, request
app = Flask(__name__)

@app.route('/search')
def search():
    # get the request query parameters as a python dict
    args = request.args.to_dict()

    # get the 'name' query parameter value with a default value as 'No Name'
    name = args.get("name", "No Name")

    return "Hello {0}!!!".format(name)

app.run(host='0.0.0.0', port=50100, debug=True)
```
### Video
The video for this post can be seen [here](https://youtu.be/-C5ZtjNwOvI)

<iframe width="560" height="315" src="https://www.youtube.com/embed/-C5ZtjNwOvI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* get variables from URL segments - https://flask.palletsprojects.com/en/2.1.x/quickstart/#variable-rules
* get variables from URL query parameters - https://stackabuse.com/get-request-query-parameters-with-flask/


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTcxMTk2Nzg3NSwtMTU4MjEzNTc2NiwtMj
A4ODc0NjYxMl19
-->