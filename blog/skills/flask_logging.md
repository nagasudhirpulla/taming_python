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
* So flask logger can be used for creating other logs also

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

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MTcyMjQ1NzUsLTE3MTc5Njg4NjIsMT
c1NzA2ODQ5XX0=
-->