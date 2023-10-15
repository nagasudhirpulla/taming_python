# heartbeat setup in windows for monitoring servers and websites

## What is heartbeat

-   **heartbeat** is a light weight agent that sends availability information to Elasticsearch database by monitoring the specified websites, IP addresses
-   The uptime of a website over HTTP or a server/device over ICMP (ping) can be continuously monitored using heartbeat
-   The availability data being stored in Elasticsearch can be easily visualized in Kibana using prebuilt dashboards and visualizations

![https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/heartbeat architecture.png?raw=true](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/heartbeat%20architecture.png?raw=true)

## Install heartbeat as a Windows background service

-   Download the heartbeat zip file from [https://artifacts.elastic.co/downloads/beats/heartbeat/heartbeat-8.10.2-windows-x86_64.zip](https://artifacts.elastic.co/downloads/beats/heartbeat/heartbeat-8.10.2-windows-x86_64.zip) or [https://www.elastic.co/guide/en/beats/heartbeat/current/heartbeat-installation-configuration.html#installation](https://www.elastic.co/guide/en/beats/heartbeat/current/heartbeat-installation-configuration.html#installation)
-   Extract the zip file and place it in C:\Program Files (like C:\Program Files\heartbeart-8.10.2)
-   Open a Powershell command line in the heartbeat folder and run the command `.\install-service-heartbeat.ps1` . If the command did not run due to script execution restriction policy, run the command `PowerShell.exe -ExecutionPolicy UnRestricted -File .\install-service-heartbeat.ps1` instead. This will allow script execution only for the current session

## Configure heartbeat

-   `heartbeat.yml` file present in the heartbeat folder can be used to configure heartbeat

### Elasticsearch connectivity

-   In `heartbeat.yml` file, configure Elasticsearch credentials and URL like the following

```yaml
output.elasticsearch:
  # Array of hosts to connect to.
  hosts: ["localhost:9200"]
  protocol: "https"
  username: "elastic"
  password: "elastic_usr_pwd"
	ssl.verification_mode: none

```

## Create heartbeat index template in Elasticsearch

-   After specifying Elasticsearch connectivity information in `heartbeat.yml` file, open a command line in the heartbeat folder and run the following command to create the index template for heartbeat data in Elasticsearch

```powershell
.\heartbeat.exe setup -e

```

## Configure heartbeat monitors

-   Each website or IP address to be monitored by heartbeat is called a **monitor**
-   Each monitor can be setup as a file in the `monitors.d` folder inside the heartbeat folder

### Setup an ICMP monitor

-   An ICMP monitor pings an IP address and stores the availability information based on the response. This can be used to track the uptime of servers or devices by pinging them continuously with their IP address
-   Create a new yml file in the monitors.d folder (say device1.yml) and specify the monitor information like below

```yaml
- type: icmp # monitor type `icmp` (requires root) uses ICMP Echo Request to ping
  # ID used to uniquely identify this monitor in elasticsearch even if the config changes
  id: my-icmp-monitor

  # Human readable display name for this service in Uptime UI and elsewhere
  name: My ICMP Monitor
  enabled: true

  # Configure task schedule using cron-like syntax
  schedule: '@every 5s' # every 5 seconds from start of beat

  # List of hosts to ping
  hosts: ["192.168.19.4"]

  # Configure IP protocol types to ping on if hostnames are configured.
  # Ping all resolvable IPs if `mode` is `all`, or only one IP if `mode` is `any`.
  ipv4: true
  ipv6: false
  mode: any

  # Total running time per ping test.
  timeout: 16s
  # Waiting duration until another ICMP Echo Request is emitted.
  wait: 1s

```

-   A new file can be created for each monitor or multiple monitors (like a device group) can also be specified in a single yml file as shown below

```yaml
- type: icmp 
  id: my-device1
  name: "Device1 Ping"
  schedule: '@every 300s'
  hosts: ["192.168.19.4"]
  ipv4: true
  ipv6: false
  mode: any
  timeout: 16s
  wait: 1s

- type: icmp 
  id: my-device2
  name: "Device2 Ping"
  schedule: '@every 300s'
  hosts: ["192.168.19.12"]
  ipv4: true
  ipv6: false
  mode: any
  timeout: 16s
  wait: 1s

```

### Setup a HTTP monitor

-   A HTTP monitor records the availability and other statistics (like latency, response status code etc.) of a desired HTTP URL
-   Create a new yml file in the monitors.d folder and specify the monitor information like shown below

```yaml
- type: http
  # ID used to uniquely identify this monitor in elasticsearch even if the config changes
  id: site1-http-monitor
  
  # Human readable display name for this service in Uptime UI and elsewhere
  name: "Site 1"
  enabled: true
  schedule: '@every 5s' # every 5 seconds from start of beat
  
  hosts: ["https://example.com"]

  # Ping all resolvable IPs if `mode` is `all`, or only one IP if `mode` is `any`.
  ipv4: true
  ipv6: false
  mode: any

  timeout: 16s

```

-   A new file can be created for each monitor or multiple monitors (like a site group) can also be specified in a single yml file as shown below

```yaml
- type: http
  id: site1-http-monitor
  name: "Site 1"
  enabled: true
  schedule: '@every 300s'
  hosts: ["https://example.com"]
  ipv4: true
  ipv6: false
  mode: any
  timeout: 16s

- type: http
  id: site2-http-monitor
  name: "Site 2"
  enabled: true
  schedule: '@every 300s'
  hosts: ["https://www.google.com"]
  ipv4: true
  ipv6: false
  mode: any
  timeout: 16s

```

## Start or stop heartbeat service

-   heartbeat service can be easily managed from the **Services** windows app
-   Start heartbeat service using the command `sc start heartbeat`
-   Stop heartbeat service using the command `sc stop heartbeat`
-   See heartbeat service status using the command `sc query heartbeat`

## Load pre-built Kibana dashboards from uptime-contrib repository

-   Go to the GitHub repository [https://github.com/elastic/uptime-contrib](https://github.com/elastic/uptime-contrib) and download the `http_dashboard.ndjson` from the dashboards→7.x folder of the GitHub repository
-   In Kibana, open Stack Management from the left menu and then select **Saved Objects** from the left menu
-   Import the `http_dashboard.ndjson` file in the Saved Objects page. Now prebuilt dashboards, visualizations, index patterns are loaded into Kibana from the `http_dashboard.ndjson` file

![https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/heartbeat dashboard.png?raw=true](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/heartbeat%20dashboard.png?raw=true)

## View heartbeat dashboards and raw logs in Kibana

-   After setting up the monitors in heartbeat, the availability or uptime data can be viewed in Kibana
-   Open Kibana and use the prebuilt dashboard Heartbeat HTTP monitoring. This dashboard is loaded from the `http_dashboard.ndjson` file.
-   View raw logs in the Kibana **Discover** section by selecting the `heartbeat-*` index pattern
-   The **Observability** section in Kibana can be used to see the heartbeat monitors information in a rich and intuitive UI

![https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/heartbeat raw logs.png?raw=true](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/heartbeat%20raw%20logs.png?raw=true)

![https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/heartbeat observability tab.png?raw=true](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/heartbeat%20observability%20tab.png?raw=true)

## Manage heartbeat index settings in Kibana

-   By default, heartbeat data is stored as a datastream in Elasticsearch. The data stream can be managed in **Index Management** page of **Stack Management** section in Kibana . A datastream named heartbeat can be seen in the **Data Streams** tab of Index Management page
-   The number of replicas of heartbeat index can be controlled in the Index Settings tab of the Index Template editing ****page. The index template can be found in the **Index Management** page. In the index settings JSON, add `"number_of_replicas": "0”`
-   If required, heartbeat data can be stored in indexes instead of datastreams. In the Logistics tab of index template editing screen, uncheck create datastream checkbox. Also in the Index settings tab of the Index template editing page, make sure that `"rollover_alias"` is defined.
-   In the **Index Lifecycle Policies** page, search for heartbeat index policy for managing the index life cycle. Data retention, compression etc. can be achieved with index lifecycle policy editing

![https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/Kibana Index Management page.png?raw=true](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/Kibana%20Index%20Management%20page.png?raw=true)

![https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/Kibana Index template editing page.png?raw=true](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/Kibana%20Index%20template%20editing%20page.png?raw=true)
### Video
Video on this post can be seen [here](https://youtu.be/sj4XF0ZRY-g?si=8FSInMc1XdJlx2W3)

<iframe width="560" height="315" src="https://www.youtube.com/embed/sj4XF0ZRY-g?si=8FSInMc1XdJlx2W3" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## References

-   Official installation guide - [https://www.elastic.co/guide/en/beats/heartbeat/current/heartbeat-installation-configuration.html](https://www.elastic.co/guide/en/beats/heartbeat/current/heartbeat-installation-configuration.html)
-   Elasticsearch connectivity options in heartbeat.yml - [https://www.elastic.co/guide/en/beats/heartbeat/current/elasticsearch-output.html](https://www.elastic.co/guide/en/beats/heartbeat/current/elasticsearch-output.html)
-   heartbeat yml reference configuration - [https://www.elastic.co/guide/en/beats/heartbeat/current/heartbeat-reference-yml.html](https://www.elastic.co/guide/en/beats/heartbeat/current/heartbeat-reference-yml.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMDMzMDMzMzIsLTg4MDg4MzI3N119
-->