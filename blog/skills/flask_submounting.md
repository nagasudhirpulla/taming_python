## Skill - Sub mounting a flask application under a URL prefix

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to sub-mount a flask application under a URL prefix

## Use cases
* mounting an application under a url prefix can help in dispatching multiple python applications  

### extract variables from URL segments
```py
from flask import Flask
from markupsafe import escape

app = Flask(__name__)

@app.route('/hello/<uname>')
def hello(uname):
    # uname variable extracted from url segment
    # sanitize the variable string using markupsafe
    sanitizedName = escape(uname)
    return "Hello {0}".format(sanitizedName)

@app.route('/echoNum/<int:num>')
def echoNum(num):
    # num integer variable is extracted from url segment
    return "The number was {0}".format(num)

@app.route('/echoPath/<path:pathVar>')
def echoPath(pathVar):
    # pathVar variable of type path is extracted from url segments
    return "The path was {0}".format(pathVar)

app.run(host='0.0.0.0', port=50100, debug=True)
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
eyJoaXN0b3J5IjpbLTE2NzU3NTQ3NzgsLTIwODg3NDY2MTJdfQ
==
-->