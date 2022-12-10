## Skill - Logging in flask
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
* So flask logger can be used to create logs inside request handlers

## Basic logging in flask
* Configure the root logger before creating the flask application
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

## Inject contextual information into logs using custom formatter
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

## access app logger inside blueprints and extensions using current_app
* The flask application variable may not be available in the blueprints or extensions python files
* The app variable can be accessed in such cases using the `current_app` variable from flask as shown below
* Note that the `current_app` variable can be available only in the context of a request

```py
# importing current_app from flask
from flask import current_app

@api.route("/info")
def api_route1():
    current_app.logger.info("called from api ")

```

## Add context in a single log using "extra"
```py
import logging
import os

logging.basicConfig(level=logging.INFO,
                    format="%(asctime)s - %(pid)s - %(org_name)s - %(levelname)s - %(message)s")
logger = logging.getLogger("root")

logger.info("Hello World!!!", extra={"org_name": "Acme", "pid": os.getpid()})
```
* In the above example, the log format is configured to show additional attributes named `pid`, `org_name` along with the message
* The additional attributes are supplied at the time of logging as a dictionary using the `extra` argument

## Add context data in all logs using "LoggerAdapter"
* Using the `extra` input argument for generating each log is susceptible to human errors
* So we can use a `LoggerAdapter` to create a logger that can add context information to all the logs by default

```py
import logging
from logging import LoggerAdapter, StreamHandler

# create a logger object
logger = logging.getLogger("root")
logger.setLevel(logging.INFO)

# create a log handler, set the log format and add to the logger object
consoleHandler = StreamHandler()
fmt = "%(asctime)s - %(org_name)s - %(levelname)s - %(message)s"
consoleHandler.setFormatter(logging.Formatter(fmt))
logger.addHandler(consoleHandler)

# create a logger adapter with the logger object
loggerAdapter = LoggerAdapter(logger, extra={"org_name": "Acme"})

# generate logs using the logger adapter
loggerAdapter.info("Hello World!!!")

```

* In the above example, the context is configured once and need not be mentioned explicitly in each log
* This can help to generate logs with context in a clean and less error prone way

### Global logger adapter for usage across multiple files
* A practical python application can contain more than one file and logs can be generated in more than one python file
```py
## app_logger.py
import logging
from logging import LoggerAdapter

class AppLogger:
    __instance: LoggerAdapter = None

    @staticmethod
    def getInstance():
        """ Static access method. """
        if AppLogger.__instance == None:
            AppLogger.initLogger()
        return AppLogger.__instance

    @staticmethod
    def initLogger():
        # get a named global logger
        appLogger = logging.getLogger("root")
        appLogger.setLevel(logging.INFO)

        # configure console logging
        streamHandler = logging.StreamHandler()
        fmt = "%(asctime)s - %(org_name)s - %(levelname)s - %(message)s"
        streamHandler.setFormatter(logging.Formatter(fmt))
        appLogger.addHandler(streamHandler)

        # setup the static variable
        AppLogger.__instance = LoggerAdapter(
            appLogger, extra={"org_name": "Acme"})

```

```py
# index.py
from app_logger import AppLogger

logger = AppLogger.getInstance()
logger.info("Hello World!!!")
```

* In the above example, a python file named `app_logger.py` exposes a class named `AppLogger` that maintains a global logger adapter instance that can be accessed from multiple python files just by calling `AppLogger.getInstance()` 
* This `AppLogger` class uses static methods and static variables for maintaining a single global logger adapter object

### Video
You can see the video for this post [here](https://youtu.be/CrCAYS37QZA)

<iframe width="560" height="315" src="https://www.youtube.com/embed/CrCAYS37QZA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

## References
* Flask logging documentation - https://flask.palletsprojects.com/en/2.2.x/logging/
* logging cookbook - https://docs.python.org/3/howto/logging-cookbook.html#using-loggeradapters-to-impart-contextual-information
* Official documentation - https://docs.python.org/3/library/logging.html
* Access flask logger inside blueprint - https://stackoverflow.com/questions/16994174/in-flask-how-to-access-app-logger-within-blueprint

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NzA1NDEwNzgsLTE1NjE2MzYwMzIsLT
cyMDg0NjQ3NCwxNjIwNTI0MDUsMTgzOTMzNzM2NCwtMTMxMDgw
MDA3OSwtMTcxNzk2ODg2MiwxNzU3MDY4NDldfQ==
-->