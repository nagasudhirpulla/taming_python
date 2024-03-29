## Skill - Logging in python flask applications
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Logging in Python](https://nagasudhir.blogspot.com/2022/11/logging-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr>

In this post we will learn how to customize logging in python flask applications

* Logging is very important in web applications
* Flask applications use standard python logging module
* Flask logger can be to create application logs instead of using a separate logger object

## Basic logging in flask
* Configure the root logger before creating the flask application, this is because, while instantiating a flask web application, the handlers of the root logger will be copied by the flask logger

```py
from flask import Flask
import logging

# One line configuration like this can also be used
# logging.basicConfig(filename="logs.log", format="%(levelname)s:%(name)s:%(message)s")

# get the root logger
logger = logging.getLogger()

# create a formatter object
logFormatter = logging.Formatter("%(levelname)s:%(name)s:%(message)s")

# add console handler to the root logger
consoleHanlder = logging.StreamHandler()
consoleHanlder.setFormatter(logFormatter)
logger.addHandler(consoleHanlder)

# add file handler to the root logger
fileHandler = logging.FileHandler("logs.log")
fileHandler.setFormatter(logFormatter)
logger.addHandler(fileHandler)

# create flask application
app = Flask(__name__)

@app.route("/")
def hello():
    # using logger inside the route handler
    app.logger.info("This is from a route handler...")
    return "Hello World!!!"

# run the flask application
app.run(host="0.0.0.0", port=50100, debug=True)

``` 

## Inject contextual information into logs using custom log formatter
```py
from flask import has_request_context, request, Flask
import logging

# using custom formatter to inject contextual data into logging
class RequestFormatter(logging.Formatter):
    def format(self, record):
        if has_request_context():
            record.url = request.url
            record.remote_addr = request.remote_addr
        else:
            record.url = None
            record.remote_addr = None
        return super().format(record)

formatter = RequestFormatter(
    '[%(asctime)s] %(remote_addr)s requested %(url)s\n'
    '%(levelname)s in %(module)s: %(message)s'
)

logger = logging.getLogger()
consoleHandler = logging.StreamHandler()
consoleHandler.setFormatter(formatter)
logger.addHandler(consoleHandler)

app = Flask(__name__)

@app.route("/")
def home():
    app.logger.info("Calling from request handler...")
    return "Hello World!!!"

app.run(host="0.0.0.0", port=50100, debug=True)

```
* In the above example, a custom formatter is used to inject request related data into the logs
* Notice that the method `has_request_context` is used to know whether the flask application context is setup while logging. This way, the formatter can be aware of the presence of a flask request

## access app logger inside blueprints or extensions using current_app
* The flask application variable may not be available in the blueprints or extensions python files
* The app variable can be accessed in such cases using the `current_app` variable from flask as shown below
* Note that the `current_app` variable can be available only in the context of a request

```py
# this is an example blueprint python file
from flask import Blueprint, current_app

api = Blueprint('codes')

@api.route("/info")
def api_route1():
    current_app.logger.info("called from api route method1 inside blueprint")
    return "Hello World!!!"

```

### Video
The video for this post can be seen [here](https://youtu.be/_Nq_n6Uk8WA)

<iframe width="560" height="315" src="https://www.youtube.com/embed/_Nq_n6Uk8WA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

## References
* Flask logging documentation - https://flask.palletsprojects.com/en/2.2.x/logging/
* logging cookbook - https://docs.python.org/3/howto/logging-cookbook.html#using-loggeradapters-to-impart-contextual-information
* Official documentation - https://docs.python.org/3/library/logging.html
* Access flask logger inside blueprint - https://stackoverflow.com/questions/16994174/in-flask-how-to-access-app-logger-within-blueprint

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3ODQ1NTI1MDQsMTU4OTI2MTQxNywyMj
UzMDk2NDIsMTcwMjIyNTQxMywtOTU1MTA0MTkwLDQ3MjM2MDg4
OCwtODkwMTIzMTc5LC0xNTYxNjM2MDMyLC03MjA4NDY0NzQsMT
YyMDUyNDA1LDE4MzkzMzczNjQsLTEzMTA4MDAwNzksLTE3MTc5
Njg4NjIsMTc1NzA2ODQ5XX0=
-->