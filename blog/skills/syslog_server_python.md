## Skill - Simple and customizable Syslog server in python

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr>

In this post we will create a Syslog server in python that listens for syslogs over the network

## What is Syslog
* Syslog is a standard protocol to send logs or event messages to a logs storage server
* A blog-post on setting a third party simple Syslog server in Windows or Ubuntu like systems can be found [here](https://nagasudhir.blogspot.com/2023/01/simple-syslog-server-setup-in-windows.html) 

## Use cases
* A Syslog server written in python can be used for the following 
	* Create a Syslog storage solution with out installing a third party software 
	* Perform ad-hoc automation upon receiving Syslog messages
	* Create data pipelines

## Minimal Syslog server in python
* Running the following python code listens for UDP requests over a specified host and port and then just logs them into a file named `logs.log` using python `logging` and `socketserver` modules

```py
## Minimal Syslog Server in Python.
import logging
import socketserver

LOG_FILE_PATH = 'logs.log'
HOST, PORT = "0.0.0.0", 514

logging.basicConfig(level=logging.INFO, format='%(message)s', filename=LOG_FILE_PATH, filemode='a')

class SyslogUDPHandler(socketserver.BaseRequestHandler):
	def handle(self):
		data = bytes.decode(self.request[0].strip())
		# socket = self.request[1]
		print( "%s: " % self.client_address[0], str(data))
		logging.info(str(data))

if __name__ == "__main__":
	try:
		server = socketserver.UDPServer((HOST,PORT), SyslogUDPHandler)
		server.serve_forever(poll_interval=0.5)
	except (IOError, SystemExit):
		raise
	except KeyboardInterrupt:
		print ("Crtl+C Pressed. Shutting down.")

```

## Testing the Syslog server by sending logs to it
* Logs can be sent to Syslog server using python
* SysLogHandler class in python logging module can be used for this purpose as shown in the below example 

```py
import logging
from logging.handlers import SysLogHandler

sysloghHandlr = SysLogHandler(address=("127.0.0.1", 514))

logger = logging.getLogger()
logger.addHandler(sysloghHandlr)
logger.setLevel(logging.INFO)

logger.info("This is a sample info message")
logger.warning("Sample warning message")

```
* By running the above script, Syslogs can be sent to a Syslog server. In this example, two Syslogs of levels `INFO` and `WARNING` are sent to a Syslog server listening over UDP 514 port with hostname '127.0.0.1' (localhost)

## Syslog server with log rotation and compression
```py
"""
Syslog Server for collecting logs
and saving in a rolling time log files
"""
import json
import logging
import os
import socketserver
import zipfile
from logging import LoggerAdapter
from logging.handlers import TimedRotatingFileHandler

# load configuration from json file
appConfig = json.load(open('config.json'))

logFilePath = appConfig["logFilePath"]
HOST, PORT = appConfig["host"], appConfig["port"]
backUpCount = appConfig["numFilesRetention"]
fileRollingHrs = appConfig["rollOverHours"]


def getFileLogger(name: str, fPath: str, backupCount: int, numRollingHrs: int) -> LoggerAdapter:
    # create a logger object and set minimum log level
    logger = logging.getLogger(name)
    logger.setLevel(logging.INFO)

    # create log handlers
    fileHandler = TimedRotatingFileHandler(
        fPath, backupCount=backupCount, when='h', interval=numRollingHrs)
    # streamHandler = logging.StreamHandler()

    # setup log rotation for file based log handler
    fileHandler.namer = lambda name: name.replace(".log", "") + ".zip"

    # setup log file compression with custom log rotation method
    def rotator(source, dest):
        zipfile.ZipFile(dest, 'w', zipfile.ZIP_DEFLATED).write(
            source, os.path.basename(source))
        os.remove(source)
    fileHandler.rotator = rotator

    # setup log formatting for log handler
    logFormatter = logging.Formatter("%(message)s")
    fileHandler.setFormatter(logFormatter)
    # streamHandler.setFormatter(logFormatter)

    # add log handler to the logger object
    logger.addHandler(fileHandler)
    # logger.addHandler(streamHandler)

    # create logger adapter with the logger object to inject extra data if required
    loggerAdapter = logging.LoggerAdapter(logger, extra={})

    # return the logger adapter
    return loggerAdapter


logger = getFileLogger(
    "app_logger", logFilePath, backUpCount, fileRollingHrs)


class SyslogUDPHandler(socketserver.BaseRequestHandler):
    def handle(self):
        data = bytes.decode(self.request[0].strip())
        # socket = self.request[1]
        strData = str(data)
        # print("%s : " % self.client_address[0], strData)
        logger.info(strData)


if __name__ == "__main__":
    try:
        server = socketserver.UDPServer((HOST, PORT), SyslogUDPHandler)
        server.serve_forever(poll_interval=0.5)
    except (IOError, SystemExit):
        raise
    except KeyboardInterrupt:
        print("Crtl+C Pressed. Shutting down.")

```

## Run the Syslog server as a windows background service with nssm 

<hr/>

## References
* Syslog Watcher download page - https://ezfive.com/syslog-watcher/downloads/
* Install and configure rsyslog server in Ubuntu - https://computingforgeeks.com/configure-rsyslog-centralized-log-server-on-ubuntu/

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU5MTE5ODExMCwtMzUwOTIzOTI4LDQ2OT
I4NTE3LC0xODk2MDkzNzMwLC0xMzU3MzQ4ODAzXX0=
-->