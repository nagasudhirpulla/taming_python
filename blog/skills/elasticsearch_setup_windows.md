# Setup Elasticsearch in Windows

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

### Prerequisites
* [Elasticsearch database introduction and terminology](https://nagasudhir.blogspot.com/2023/08/elasticsearch-database-concepts.html)

<hr>

- In this post we will setup a simple single-node Elasticsearch database in windows using the Elasticsearch zip file
- Elasticsearch database can be installed to run as a windows service like any other database like Oracle or PostgreSQL

## Step 1 - Download Elasticsearch

- Download Elasticsearch zip file for Windows from [https://www.elastic.co/downloads/elasticsearch](https://www.elastic.co/downloads/elasticsearch)
- Extract the Elasticsearch folder and place in C drive. For example `C:\elasticsearch-8.10.2`

## Run Elasticsearch from command line (not recommended)

- Open a command prompt in the Elasticsearch folder
- Run Elasticsearch using the command `.\bin\elasticsearch.bat`
- Closing the command line will stop Elasticsearch. Hence it is recommended to run Elasticsearch as a windows service

## Step 2 - Run Elasticsearch as a windows background service

- Open a command prompt in the Elasticsearch folder
- Run the command `.\bin\elasticsearch-service.bat install` to install the Elasticsearch windows service
- Run the command `.\bin\elasticsearch-service.bat start` to start the Elasticsearch database
- Run the command `.\bin\elasticsearch-service.bat stop` to stop the database if required
- Run the command `.\bin\elasticsearch-service.bat remove` to uninstall the database service if required

## Step 3 - Reset the 'elastic' user password

- Open a command prompt in the Elasticsearch folder
- Run the command `.\bin\elasticsearch-reset-password.bat -i -u elastic` and reset the password of ***elastic*** user

## Step 4 - Check if Elasticsearch is running

- Go to a web browser and open the URL [https://localhost:9200](https://localhost:9200)
- Enter the username and password of the ***elastic*** user
- Elasticsearch database details should be displayed. This means that the database is running with the desired ***elastic*** user credentials

## Change the folder where data is stored
* By default Elasticsearch data is stored in the data folder of Elasticsearch folder
* Additional data folders or modification of existing data folder can be done using the `elasticsearch.yml` file  
* Open `elasticsearch.yml` file in the config folder of Elasticsearch folder
* Search for `path.data` and set it to a single data folder or multiple data folder paths. For example, you can write  `path.data: C:\elasticsearch-8.10.2\data` or 

## Set the memory limit of Elasticsearch windows service

- By default only 1 GB is allotted to elasticsearch windows service which can result in errors while running multiple queries or large data queries.
- The memory limit of elasticsearch windows service can be increased for this purpose
- Open a command prompt in the Elasticsearch folder
- Run the command `.\bin\elasticsearch-service.bat manager`. A configuration window will appear
- Go to ***Java*** tab and set the initial and maximum memory pool values to higher values, say 10 GB (=10240 MB)

## Disable HTTPS (Optional)

- Open `elasticsearch.yml` file in the config folder of Elasticsearch folder
- In the `xpack.security.http.ssl` section, set `enabled: false` to disable HTTPS

## Restrict Elasticsearch access to remote connections (Optional)

- Open `elasticsearch.yml` file in the config folder of Elasticsearch folder
- Set `http.host: localhost` to disable remote http connections to Elasticsearch. If required LAN IP address can also be used in http.host to restrict the access to only LAN

## Change the Elasticsearch port (Optional)

- By default Elasticsearch runs on port 9200
- Open `elasticsearch.yml` file in the config folder of Elasticsearch folder
- Change http.port to the desired value if required

### References

- Elasticsearch official docs for installation - [https://www.elastic.co/guide/en/elasticsearch/reference/current/zip-windows.html](https://www.elastic.co/guide/en/elasticsearch/reference/current/zip-windows.html)
- Elasticsearch configuration official docs - [https://www.elastic.co/guide/en/elasticsearch/reference/current/settings.html](https://www.elastic.co/guide/en/elasticsearch/reference/current/settings.html)
- difference between http.host and network.host in Elasticsearch configuration - [https://discuss.elastic.co/t/difference-between-network-host-transport-host-and-http-host-settings/308215/2](https://discuss.elastic.co/t/difference-between-network-host-transport-host-and-http-host-settings/308215/2)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzM1NTg0MzM5LDE5NDA0MTc0MzFdfQ==
-->