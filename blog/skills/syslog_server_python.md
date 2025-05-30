## Skill - Simple and customizable Syslog server in python

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr>

In this post we will create a Syslog server in python that listens for Syslogs over the network and logs them to file storage

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
* The `handle` function inside the `SyslogUDPHandler` class has access to the Syslogs upon receiving by the socketserver.


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
* The above python file `server.py` runs like a Syslog server. It requires a configuration file named `config.json` where all the configuration can be specified. The `config.json` file should be in the same folder as `server.py`

```json
{
    "_comment": "This is the config.json file",
    "logFilePath": "app_log.log",
    "host": "0.0.0.0",
    "port": 514,
    "numFilesRetention": 400,
    "rollOverHours": 24
}
```

* The above python script will listen for Syslog messages and write them into a log file. The log file location and Syslog server listening port can be configured in `config.json` file
* The log files will be rotated and compressed after the configured number of hours. The number of hours can be configured in the `config.json` file
* The number of files after which the old log files can be deleted can be configured in the `config.json` file
* A detailed blog-post on logging in python with log rotation and compression can be found [here](https://nagasudhir.blogspot.com/2022/11/logging-in-python.html)
* The above example rotates logs based on time. But this code can be customized to make the logs rotate based on size using the `RotatingFileHandler` class

## Run the Syslog server as a windows background service with nssm
* Create a batch file named `run_server.bat` and write the following in it

```bash
REM batch script to run the syslog server
python run_server.py
```

* Use nssm to run this batch script as a windows background service
* Open the command prompt in administrative mode and run the command `nssm install syslog_server_python`
* After the service is installed, open `services.msc` and make the startup type of this service as 'Automatic', so that the service will start upon system reboot
* A blog-post on using nssm to run a script as a windows background service can be found [here](https://nagasudhir.blogspot.com/2022/09/run-python-flask-server-as-windows.html)

## Conclusion
* The python based Syslog server once setup, is quite robust without many external python library dependencies and can be used for small scale monolithic deployments
* However, for complex and critical Syslog server deployments, battle-tested and robust syslog server solutions like `rsyslog` can be used 

### Video
The video for this post can be seen [here](https://youtu.be/r3fGPk8ga9E)

<iframe width="560" height="315" src="https://www.youtube.com/embed/r3fGPk8ga9E" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

<hr/>

## References
* Docs on logging - https://docs.python.org/3/library/logging.html
* Docs on nssm - https://nssm.cc/usage
* Install and configure rsyslog server in Ubuntu - https://computingforgeeks.com/configure-rsyslog-centralized-log-server-on-ubuntu/

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI3OTg0MTIyNiwxMDMyMjM4MzY2LC0xNz
U3NzQ5NDg3LDIxMTEwMTg1MDksLTIxMzEwNDA0OSwzODc5Mzk1
NzIsLTEzMjM3OTQ4MjMsLTExMjk1MzMyNDAsLTE2MjcyOTg0NT
IsLTE2MTg5MDU0ODMsLTM1MDkyMzkyOCw0NjkyODUxNywtMTg5
NjA5MzczMCwtMTM1NzM0ODgwM119
-->