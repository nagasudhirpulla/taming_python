## Skill - Simple syslog server setup in Windows and Ubuntu

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr>

In this post we will setup a simple syslog server in windows and Debian based systems like Ubuntu

## What is Syslog
Syslo 

## Simple Syslog server setup in windows
* Syslog Watcher is a free Syslog listener for windows that view logs from various syslog sources
* Configure the Syslog Watcher to listen for syslogs at UDP port 514

![syslog watcher config demo.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/syslog%20watcher%20config%20demo.png)
## Syslog server setup in Ubuntu or Debian based systems
* rsyslog server is a robust opensource syslog server in ubuntu that can store logs in log files
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

<hr/>

## References
* Syslog Watcher download page - https://ezfive.com/syslog-watcher/downloads/
* Install and configure rsyslog server in Ubuntu - https://computingforgeeks.com/configure-rsyslog-centralized-log-server-on-ubuntu/

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyNjA0NTExMDBdfQ==
-->