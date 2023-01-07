## Skill - Send logs to Syslog server in Python using SysLogHandler

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Logging in Python](https://nagasudhir.blogspot.com/2022/11/logging-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr>

* In this post we will learn how to send logs to a syslog server from python using python logging module and SysLogHandler
* A simple syslog server can be setup in windows or Debian based systems like Ubuntu as shown in [this](https://nagasudhir.blogspot.com/2023/01/simple-syslog-server-setup-in-windows.html) blogpost

## Python code to send logs to Syslog server 
* SysLogHandler of python logging module can be used to send logs to syslog server

```py
import logging
from logging.handlers import SysLogHandler

remoteHost = '127.0.0.1'
remotePort = 514

logger = logging.getLogger()
logger.setLevel(logging.INFO)
logger.addHandler(SysLogHandler(address=(remoteHost, remotePort)))

logger.info("Hello World!!!")
logger.error("This is error message")

```

* As shown in the above example, the SysLogHandler is configured to send logs to syslog server running at host '127.0.0.1' and UDP port 514

<hr/>

## References
* Documentation - https://docs.python.org/3/library/logging.handlers.html#sysloghandler

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjk3Mjk3MDE1LC0zNzkxMDQ3MTgsLTEwNT
IyMjEzNzAsLTEzMDA0MzUwLDQ3Mzc4MzYxMywtMTMyMTMxNTgw
OSwtMTkyNDQ5NTg2Myw3NDUyNTAwNTAsLTEwMDc4OTI4MzMsLT
YyNzc4NDUxOCwtODgwMzU1Nzc4LC0xMjUwMjU3MTc3XX0=
-->