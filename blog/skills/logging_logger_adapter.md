## Skill - Logging with contextual data using LoggerAdapter in Python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Logging in Python](https://nagasudhir.blogspot.com/2022/11/logging-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr>

In this post we will learn how to add extra contextual data to logs using LoggerAdapter in python 

## Use cases
* Adding contextual data in logs may be useful for easy debugging of the logs and also add new attributes for efficient querying and filtering of the logs 
* For example if additional attributes like process Id, application name, etc. are added in each log, searching and debugging logs can be more efficient

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

### global logger adapter for usage across multiple files
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
* This `AppLogger` class uses static methods and static variables for maintaining a single logger adap

<hr/>

## References
* logging cookbook - https://docs.python.org/3/howto/logging-cookbook.html#using-loggeradapters-to-impart-contextual-information
* Official documentation - https://docs.python.org/3/library/logging.html

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkxMTUzMzg5NCwtMzk0NzMyODU4LC0yNj
M0NDkyMDYsMTMyMzY4NTg3OCw5NDI2OTA5OTQsLTEwMjczNDU4
MjUsLTU4OTQ1NjUyM119
-->