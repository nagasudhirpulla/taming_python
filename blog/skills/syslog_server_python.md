## Skill - Simple and customizable Syslog server in python

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr>

In this post we will create a Syslog server in python that listens for syslogs over the network

## What is Syslog
* Syslog is a standard protocol to send logs or event messages to a logs storage server
* A blog-post on setting a third party simple Syslog server in Windows or Ubuntu like systems can be found [here](https://nagasudhir.blogspot.com/2023/01/simple-syslog-server-setup-in-windows.html) 

## Use case
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



## Syslog server setup in Ubuntu or Debian based systems
* rsyslog server is a robust production-ready opensource syslog server in ubuntu that can store logs in log files
* rsyslog can be installed in ubuntu using the following command
```bash
sudo apt-get install rsyslog -y or sudo apt install rsyslog -y
```
* rsyslog server can be started and enabled to start at system startup using the following commands
```bash
sudo systemctl start rsyslog
sudo systemctl enable rsyslog
```
* rsyslog server can be configured using the configuration file located at `/etc/rsyslog.conf` 
* Make sure the following lines are present in the configuration file for listening at UDP port 514
```bash
module(load="imudp")
input(type="imudp" port="514")
```
* Make sure the following lines are present in the configuration file below the listener configuration for specifying the logs storage files location
```bash
$template remote-incoming-logs,"/var/log/%HOSTNAME%/%PROGRAMNAME%.log" 
*.* ?remote-incoming-logs
& ~
```
* rsyslog server can be restarted after configuration changes using the following command
```bash
sudo systemctl restart rsyslog
```
* rsyslog server status can be checked using the following command
```bash
sudo systemctl status rsyslog
```
* If firewall is used in the server, allow listening on UDP 514 port using the following command
```bash
sudo ufw allow 514/udp
```

### Video
The video for this post can be seen [here](https://youtu.be/TIis6_RmMJo)

<iframe width="560" height="315" src="https://www.youtube.com/embed/TIis6_RmMJo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

<hr/>

## References
* Syslog Watcher download page - https://ezfive.com/syslog-watcher/downloads/
* Install and configure rsyslog server in Ubuntu - https://computingforgeeks.com/configure-rsyslog-centralized-log-server-on-ubuntu/

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTEyMjc3MTAwMiwtMTM1NzM0ODgwM119
-->