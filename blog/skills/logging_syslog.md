## Skill - Logging to Syslog server in Python

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Logging in Python](https://nagasudhir.blogspot.com/2022/11/logging-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr>

In this post we will learn how to send logs to a syslog server from python using python logging module and SysLogHandler

## Example
* Just like StreamHandler sends logs to console and FileHandler sends logs to files, SysLogHandler can be used to send logs to syslog server

```py
import logging
from logging.handlers import SysLogHandler

syslogHost = '127.0.0.1'
syslogPort = 514

logger = logging.getLogger()
logger.setLevel(logging.INFO)
logger.addHandler(SysLogHandler(address=(syslogHost, syslogPort)))

logger.info("Hello World!!!")
logger.error("This is error message")
```

* As shown in the above example, the SysLogHandler is configured to send logs to syslog server running at host '127.0.0.1' and UDP port 514

## Simple Syslog server setup in windows
* Syslog Watcher is a free Syslog listener for windows that can be used to view logs from various log sources
* Configure the
![syslog watcher config demo.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/syslog%20watcher%20config%20demo.png)

<hr/>

## References
* Syslog Watcher download page - https://ezfive.com/syslog-watcher/downloads/

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTc1NzY4ODY0LC0xOTI0NDk1ODYzLDc0NT
I1MDA1MCwtMTAwNzg5MjgzMywtNjI3Nzg0NTE4LC04ODAzNTU3
NzgsLTEyNTAyNTcxNzddfQ==
-->