### What is filebeat

-   filebeat is an agent that can ship logs from files into Elasticsearch
-   filebeat can be installed as a windows background service that sends logs from various files or syslog into Elasticsearch

![filebeat_architecture.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/filebeat_architecture.png?raw=true)

## Install filebeat in windows

-   Download filebeat zip file from [https://www.elastic.co/downloads/beats/filebeat](https://www.elastic.co/downloads/beats/filebeat)
-   Extract filebeat contents from zip file into a folder `C:\Program Files\Filebeat`
-   Open a command prompt with administrative privileges in the folder `C:\Program Files\Filebeat` and run the command `.\install-service-filebeat.ps1`. If script execution is disabled, run the command `PowerShell.exe -ExecutionPolicy UnRestricted -File .\install-service-filebeat.ps1` instead
-   Now filebeat is installed as a windows service

## Configure Elasticsearch and Kibana connectivity in filebeat

filebeat can be configured with `filebeat.yml` file. The reference file can be found at [https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-reference-yml.html](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-reference-yml.html)

-   Open `filebeat.yml` file in the filebeat folder
-   Search for `output.elasticsearch` section to configure Elasticsearch connectivity like the following

```yaml
output.elasticsearch:
  hosts: ["localhost:9200"]
  protocol: "https"

  # Authentication credentials - either API key or username/password.
  #api_key: "id:api_key"
  username: "elastic"
  password: "tamingpython"
  ssl.verification_mode: none

```

## Setup filebeat index template and kibana dashboards

-   Open `filebeat.yml` file in the filebeat folder
-   Search for `setup.kibana` section to configure Kibana connectivity like the following

```yaml
setup.kibana:
    host: "localhost:5601"
    protocol: "http"
    ssl.verification_mode: none
    username: "elastic"  
    password: "tamingpython"

```

-   Open a command window in the filebeat folder and run the command `.\filebeat.exe setup -e` . Now the Elasticsearch index template and sample kibana dashboards are loaded

## Configure filebeat with files as data source

-   Open `filebeat.yml` file in the filebeat folder
-   Setup files to be read can be configured in the `filebeat.inputs` section as shown below

```yaml
filebeat.inputs:
- type: filestream
	enabled: true
  id: app1-logs-id
  paths:
    - C:\path\to\required folder\*.log
	fields:
	    data_type: "text_lines"

```

-   Multiple filestream inputs can be configured under the filebeat.inputs section
-   The above example configuration sends the lines from all the `.log` files from the specified folder in real time to Elasticsearch
-   Each line of the .log files will be sent as a JSON to Elasticsearch
-   An additional field named “data” with value “text_lines_app1” will also be added to each JSON sent to Elasticsearch
-   A text file line stored as a log file is shown in the image below. The text of line can be seen in the _source.message field of JSON
-   The logs as shown in the below image can be seen in Kibana Discover page with `filebeat-*` index pattern selected

![filebeat_text_lines_demo.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/filebeat_text_lines_demo.png?raw=true)

### Parsers

-   The filestream inputs can be parsed using parsers.
-   The following example parses each line of a file as a syslog in RFC3164 format. Also, an additional JSON field named “data_type” with value “syslog” is also attached to each JSON pushed to Elasticsearch

```yaml
filebeat.inputs:
- type: filestream
  id: app2-logs-id
  enabled: true
  paths:
    - C:\Users\Nagasudhir\Documents\Python Projects\taming_python\filebeat\logs\*.txt
  parsers:
  - syslog:
      format: rfc3164
  fields:
    data_type: "syslog"

```

-   The following configuration parses each line from the file as a JSON object and places it in the “msg_json” attribute of each log. Also a JSON field named “data_type” with value “json_data” is also attached to each JSON pushed to Elasticsearch.

```yaml
- type: filestream
  id: app3-logs-id
  enabled: true
  paths:
    - C:\Users\Nagasudhir\Documents\Python Projects\taming_python\filebeat\logs\*.ndjson
  parsers:
  - ndjson:
      target: "msg_json"
  fields:
    data_type: "json_data"

```

![filebeat_json_logs_demo.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/filebeat_json_logs_demo.png?raw=true)

-   The documentation for filestream parsers can be found at [https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-input-filestream.html#_parsers](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-input-filestream.html#_parsers)
-   The documentation on filebeat filestream input can be found at [https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-input-filestream.html](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-input-filestream.html)

## Read data from syslog

-   filebeat can also read data from syslog instead of files
-   The below configuration in filebeat.yml can make filbeat listen for syslog input over udp protocol over port 9000 in rfc3164 format
-   The options and docs for syslog input can be found at [https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-input-syslog.html](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-input-syslog.html)

```yaml
filebeat.inputs:
- type: syslog
  format: rfc3164
  protocol.udp:
    host: "localhost:9000"

```

## References

-   official filebeat installation guide - [https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-installation-configuration.html](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-installation-configuration.html)
-   filebeat syslog input docs - [https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-input-syslog.html](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-input-syslog.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQwNjkyNzQ0NCwxMDQwOTUzMjAzLDIwNT
cxMDIwOTZdfQ==
-->