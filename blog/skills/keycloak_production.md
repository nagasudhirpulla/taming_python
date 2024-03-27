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
* Unzip into a folder like ``
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM2MDQxMzA2MSw3MDkxNzIyOF19
-->