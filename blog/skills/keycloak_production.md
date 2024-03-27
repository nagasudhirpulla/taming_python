# Run keycloak in production mode in windows with HTTPS

* To run keycloak in production mode, certificates and hostname are to be configured at the least
* Let us setup keycloak in windows

## Install OpenJDK
* Download OpenJDK zip file. Refer to Keycloak documentation for the minimum JDK version required for the Keycloak being installed (https://www.keycloak.org/getting-started/getting-started-zip)
* Extract the zip file to a folder like `C:\Program Files\Java\jdk-22`
* Set the environment variable named JAVA_HOME and assign the jdk folder path to it (Example  `C:\Program Files\Java\jdk-22`)
* Add the java bin folder path to the environment variable PATH (Example: `C:\Program Files\Java\jdk-22\bin`)


## Install Keycloak
* Download Keycloak zip file from https://www.keycloak.org/downloads
* Unzip into a folder like `C:\keycloak-24.0.2`
* Now Keycloak is ready to run

## Run keycloak in development mode
* Open a command prompt in the Keycloak folder
* Run the command `.\bin\kc.bat start-dev` to run Keycloak in development mode

## Run Keycloak in production mode
* Keycloak can be configured from the `conf/keycloak.conf` file present in the Keycloak folder

### Setup the Keycloak hostname
* Add the hostname information in the `keycloak.conf` file with the setting `hostname=localhost`. 
* The hostname can be localhost or IP address or hostname or domain name.
* This makes Keycloak to allow only the requests with the configured hostname
* If we desire to allow all hostnames,

### Setup the certificates
*  
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk5MTg1MDYyLDcwOTE3MjI4XX0=
-->