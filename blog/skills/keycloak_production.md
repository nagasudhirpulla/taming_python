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
* This makes Keycloak to allow only the requests with the configured hostname in the request header
* To allow all hostnames, the setting `hostname-strict=false` can be kept in the `keycloak.conf` file

### Setup the certificate
*  Keycloak requires the certificate for running in production mode
* Certificate is used by Keycloak for public and private keys
* Certificate can be taken from a certificate authority or a self-signed certificate can be generated. 
* A self-signed certificate can be generated Use openssl to generate the certificate file and key file using the below command. openssl can be accessed from a git bash. Run the below command in the conf folder of Keycloak so that the files are generated there. 
```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout kc.key.pem -out kc.crt.pem
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbNDkzMjc4MjIsMzI1OTcwMDE0LC0xODkxOT
I0NzUwLDcwOTE3MjI4XX0=
-->