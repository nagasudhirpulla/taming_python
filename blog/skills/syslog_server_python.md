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

```

<hr/>

## References
* Syslog Watcher download page - https://ezfive.com/syslog-watcher/downloads/
* Install and configure rsyslog server in Ubuntu - https://computingforgeeks.com/configure-rsyslog-centralized-log-server-on-ubuntu/

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NzUzNTA4NjYsNDY5Mjg1MTcsLTE4OT
YwOTM3MzAsLTEzNTczNDg4MDNdfQ==
-->