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

* In the above example, a 


### logging into files with basicConfig
```py
import logging

# configure logging in root logger
logging.basicConfig(format="%(asctime)s::%(levelname)s::%(message)s",
                    level=logging.INFO,
                    filename="test.log"
                    )

# create logs
logging.info("info log")
logging.warning("this is warning log")
logging.error("this is error log")
```
* Logs can be sent to a file instead of console using the `filename` input for the `basicConfig` function as shown above
* The `filename` can be a relative or absolute file path
* In the above code example, the logs will be sent to a file named `test.log` located in the same folder as the python program

### logging with logger object and log handler
```py
import logging

# create a logger object
logger = logging.getLogger("test_app")

# set the logging level
logger.setLevel(logging.INFO)

# create a streamHandler to log into console
consoleHandler = logging.StreamHandler()

# create a formatter object to specity the log format
consoleFormatter = logging.Formatter("%(asctime)s - %(levelname)s - %(message)s")

# assign the formatter to log handler
consoleHandler.setFormatter(consoleFormatter)

# add the log handler to logger object
logger.addHandler(consoleHandler)

# create logs
logger.info("Hello World!!!")

try:
    x = 1/0
except Exception as e:
    logger.error("Some error occured", exc_info=e)
```

The following steps are involved in the above program
* Create a named logger object using `getLogger` function
* Create a log handler that emits logs into console. `logging.StreamHandler` emits logs into console
* Create a formatter object to specify the log format and and assign it to the log handler
* Add the log handler to the logger object
* User logger object to generate logs

### specify log timestamp format in the formatter object
* The format of log timestamp can be explicitly mentioned in the log formatter using the `datefmt` argument as shown below
```py
# ...
# create a formatter object to specity the log format
consoleFormatter = logging.Formatter(
    "%(asctime)s - %(levelname)s - %(message)s", datefmt="%Y-%m-%d %H:%M:%S")
# ...
```
### logging into files with RotatingFileHandler
```py
import logging
from logging.handlers import RotatingFileHandler

# create a logger object names fLogger
logger = logging.getLogger("fLogger")

# set logging level
logger.setLevel(logging.INFO)

# create a log handler that dumps logs into a file named 'test.log'
# backupCount=100 means, only latest 100 log files will be retained and older log files will be deleted
# maxBytes=1024 means, new log file will be generated if log file exeeds 1024 bytes
fileHandler = RotatingFileHandler("test.log", backupCount=100, maxBytes=1024)

# use namer function of the handler to keep the .log extension at the end of the file name
fileHandler.namer = lambda name: name.replace(".log", "") + ".log"

# create a log formatter object and assign to the log handler
logFormatter = logging.Formatter(
    "%(asctime)s - %(levelname)s - %(message)s", datefmt="%Y-%m-%d %H:%M:%S")
fileHandler.setFormatter(logFormatter)

# add log handler to logger object
logger.addHandler(fileHandler)

# generate logs with logger object
logger.info("info message")
logger.warning("warn message")

try:
    x = 1/0
except Exception as e:
    logger.error("Some error occured", exc_info=e)
```
* `RotatingFileHandler` can be used if we want to logs be written to a new file after a certain file size
* The old logs will be sent to a new file after the size threshold. In the above example, the log files will be generated like test.log, test.1.log, test.2.log, ... 
* `maxBytes=1024` in `RotatingFileHandler` means, new log file will be generated if log file exceeds 1024 bytes
* `backupCount=100` in `RotatingFileHandler` means, only latest 100 log files will be retained and older log files will be deleted
* Using this approach will avoid huge log file sizes while the python scripts continuously emit logs. In some cases huge size log files (like 2GB log file) will even crash the python code

### rotate log files periodically using "TimedRotatingFileHandler"
```py
import logging
from logging.handlers import TimedRotatingFileHandler

# create a logger named fLogger
logger = logging.getLogger("fLogger")

# set logging level
logger.setLevel(logging.INFO)

# create a log handler
# backupCount=100 means, only latest 100 log files will be retained and older log files will be deleted
# interval=1 means the log rotation interval is 1
# when='d' means the rotating interval will be in terms of days
# so logs will be rotated every 24 hours(1 day) in this example
# Following are the options for 'when' parameter
# S - Seconds, M - Minutes, H - Hours, D - Days, 
# midnight - roll over at midnight, W{0-6} - roll over on a certain day; 0 - Monday
fileHandler = TimedRotatingFileHandler(
    "test.log", backupCount=100, when='d', interval=1)

# use namer function of the handler to keep the .log extension at the end of the file name
fileHandler.namer = lambda name: name.replace(".log", "") + ".log"

# create a log formatter object and assign to the log handler
logFormatter = logging.Formatter("%(asctime)s - %(levelname)s - %(message)s")
fileHandler.setFormatter(logFormatter)

# add log handler to logger object
logger.addHandler(fileHandler)

# generate logs with logger object
logger.info("info message")
logger.warning("warn message")

```
* `TimedRotatingFileHandler` can be used if we want to periodically rotate logs. This can be useful to easily trace the log files based on date or time
* The old logs will be sent to a new file after the configured time interval. In the above example, the log files will be generated like test.log, test.2022-11-14.log, ... 

### logging into multiple places with handlers
* Multiple log handlers that can send logs to multiple locations (like file, console etc.) can be added to a single logger object
* Logger object can send logs to multiple locations using this approach 
```py
import logging
from logging.handlers import RotatingFileHandler

# create a logger object names myLogger
logger = logging.getLogger("myLogger")
logger.setLevel(logging.INFO)
#################
# create a file handler that logs into a file
fileHandler = RotatingFileHandler("test.log", backupCount=100, maxBytes=1024)
fileHandler.namer = lambda name: name.replace(".log", "") + ".log"

# create a log formatter object and assign to the log handler
logFormatter = logging.Formatter(
    "%(asctime)s - %(levelname)s - %(message)s", datefmt="%Y-%m-%d %H:%M:%S")
fileHandler.setFormatter(logFormatter)

# add log handler to logger object
logger.addHandler(fileHandler)
#################
# create a stream handler that logs into console
consoleHandler = logging.StreamHandler()

# create a log formatter object and assign to the log handler
consoleHandler.setFormatter(logging.Formatter(
    "%(asctime)s - %(levelname)s - %(message)s"))

# add console handler to logger object
logger.addHandler(consoleHandler)
#################
# generate logs with logger object
logger.info("info message")
logger.warning("warn message")

try:
    x = 1/0
except Exception as e:
    logger.error("Some error occured", exc_info=e)

```
* In the above program, `fileHandler` sends logs to a file and `consoleHandler` sends logs to console
* Both handlers are added to the logger object. Hence logs can be sent to both file and console.

### compress the rotated log files to save logs storage
* Custom log rotation function can be used to customize log rotation process
* For this case, we are compressing the rotated log file as a zip file using `zipfile` python module
* This approach is very useful to save storage by compressing rotated logs 
```py
import logging
from logging.handlers import RotatingFileHandler
import os
import zipfile
from os.path import basename

# custom log rotation function to zip rotated log files
def rotator(source, dest):
    # rotated log file is zipped and the original log file will be deleted 
    zipfile.ZipFile(dest, 'w', zipfile.ZIP_DEFLATED).write(
        source, basename(source))
    os.remove(source)

# create a logger named zipLogger
logger = logging.getLogger("zipLogger")
logger.setLevel(logging.INFO)

# create log handler to store logs as files with log rotation for every 1024 bytes and retain only latest 100 log files
fileHandler = RotatingFileHandler("logs/test.log", backupCount=100, maxBytes=1024)

# set log formatting for the log handler
fileHandler.setFormatter(logging.Formatter("%(asctime)s - %(levelname)s - %(message)s"))

# setup custom log rotation function to zip rotated files
fileHandler.rotator = rotator

# rename the rotated files to have the .zip extension
fileHandler.namer = lambda name: name.replace(".log", "") + ".zip"

# add the log handler to logger
logger.addHandler(fileHandler)

# create log messages
logger.info("info message")
logger.warning("warn message")
logger.error("error message")

``` 

### Video
You can see the video for this post [here](https://youtu.be/wrpu-Qr_Yvk)

<iframe width="560" height="315" src="https://www.youtube.com/embed/wrpu-Qr_Yvk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

## References
* Official documentation - https://docs.python.org/3/library/logging.html

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTA4ODMzODg1LC0yNjM0NDkyMDYsMTMyMz
Y4NTg3OCw5NDI2OTA5OTQsLTEwMjczNDU4MjUsLTU4OTQ1NjUy
M119
-->