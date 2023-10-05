## What is Kibana

-   Kibana is the data exploration and visualization tool for the Elasticsearch database
-   Kibana for Elasticsearch is just like sqldeveloper for Oracle, pgAdmin for PostgreSQL, phpMyAdmin for MySQL
-   Interactive dashboards with customizable visualizations like line chart, bar chart, pie chart, maps, heatmap etc. can be created with Kibana over Elasticsearch data
-   Users can use Kibana to gain valuable insights on Elasticsearch data without any coding skills

## Download Kibana

-   Kibana is basically a web server. It can be downloaded as a zip file
-   It can be downloaded from [https://www.elastic.co/downloads/kibana](https://www.elastic.co/downloads/kibana)

## Create password for ‘kibana_system’ user in Elasticsearch

-   In Elasticsearch `bin` folder, run the command `elasticsearch-reset-password -i -u kibana_system` and reset the password for the “kibana_system” elasticsearch user

## Configure Kibana

-   Extract the Kibana zip file contents to C drive. For example `C:\\Kibana-8.10.2`
-   In the config folder, open `kibana.yml` file
-   The following configurations can be done in the `kibana.yml` file

### Setup Elasticsearch connectivity

-   Set the username and password of “kibana_system” user in `elasticsearch.username` and `elasticsearch.password` fields of the kibana.yml file
-   Set the Elasticsearch URL in `elasticsearch.hosts` field
-   Keep `elasticsearch.ssl.verificationMode` to `none` to skip the Elasticsearch SSL verification check

### Change the port of Kibana

-   Change the `server.port` attribute in `kibana.yml` file in the config folder to change the port on which Kibana will listen for requests. The default port for Kibana is 5601

### Control remote connections to Kibana

-   Keep the `server.host` attribute to ‘localhost’ to make remote connections not allowed
-   Keep the `server.host` attribute to the LAN IP address (like 192.168.3.26) to allow connections from local LAN

## Run Kibana from command line

-   After configuring the elasticsearch connectivity, open a command line in the bin folder of Kibana and run the command `kibana.bat`
-   This will run Kibana from the command line
-   Kibana can be checked in the browser. For example, we can open `localhost:5601` to check if Kibana is working

## Setup Kibana as a windows background service with nssm

-   Download nssm exe file from [https://nssm.cc/download](https://nssm.cc/download) and place it in C drive (Example: `C:\\nssm\\nssm.exe`)
-   Open a command line with administrative privilege in the folder with nssm.exe and run the command `nssm install kibana_service`. A popup will open to create a windows service.
-   In the `Application` tab, Enter the path of kibana.bat and the folder of kibana.bat as shown below

![https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/kibana_nssm_install_1.png?raw=true](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/kibana_nssm_install_1.png?raw=true)

-   In the `I/O` tab, enter the path of a log file where the service logs will be stored. For this purpose, create a folder in kibana folder (like `service_logs`) and create a blank log file (say `kibana_service.log`)

![https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/kibana_nssm_install_2.png?raw=true](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/kibana_nssm_install_2.png?raw=true)

-   In the `File rotation` tab, check all the boxes and enter 10485760 bytes, so that a new log file will be generated for every 5 MB of logs.

![https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/kibana_nssm_install_3.png?raw=true](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/kibana_nssm_install_3.png?raw=true)

-   Finally click the `Install service` button to create a windows service for kibana
-   Go to the `Services` app in windows, search for kibana_service service, right click and start the service
-   Right click on the service and open the properties to change the startup type as **Automatic** to make the Kibana service run automatically upon system startup
-   Verify if Kibana is running in the browser (say `localhost:5601`)

## References

-   Kibana installation guide - [https://www.elastic.co/guide/en/kibana/current/windows.html](https://www.elastic.co/guide/en/kibana/current/windows.html)
-   Kibana download page - [https://www.elastic.co/downloads/kibana](https://www.elastic.co/downloads/kibana)
-   Kibana configuration guide - [https://www.elastic.co/guide/en/kibana/current/settings.html](https://www.elastic.co/guide/en/kibana/current/settings.html)
-   Kibana install as service with sc command - [https://stackoverflow.com/questions/29261809/elastic-kibana-install-as-windows-service](https://stackoverflow.com/questions/29261809/elastic-kibana-install-as-windows-service)
-   official Kibana learning videos - [https://www.elastic.co/videos/training-how-to-series-stack?elektra=kibana-dashboard&storm=hero](https://www.elastic.co/videos/training-how-to-series-stack?elektra=kibana-dashboard&storm=hero)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI2MDE3MTMxN119
-->