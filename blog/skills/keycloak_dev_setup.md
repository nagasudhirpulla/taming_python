## Skill - Setup Keycloak as OAuth 2.0 server in Windows for testing and development

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<br>
In this post we will learn how to setup Keycloak easily on windows for development and testing purposes

- The main component of an OAuth 2.0 flow is the OAuth 2.0 server or the STS (Security Token Service)
- [Keycloak](https://www.keycloak.org/) is an open-source Identity and Access Management (IAM) solution by RedHat that can be used as an OAuth 2.0 server.
- Keycloak provides an admin UI for managing users, clients and resources
- Keycloak can run on bare-metal or Docker or Kubernetes
- Keycloak can be used to securely store the users and clients information in a central Keycloak database

## Download and install Keycloak
- Before installing keycloak, ensure OpenJDK 11 or latest is installed. OpenJDK can be downloaded and installed from [https://jdk.java.net/](https://jdk.java.net/)
- Java version installed can be verified using the command “java -version”
- Keycloak can be downloaded as a zip file from [https://www.keycloak.org/downloads](https://www.keycloak.org/downloads)
- Unzip the downloaded zip file
- Now Keycloak is ready to use for development and testing purposes

## Running Keycloak for the first time
- Open a command line in the Keycloak folder
- run the command “.\bin\kc.bat start-dev”
- Now Keycloak admin UI should be accessible in the browser at http://localhost:8080
- If the Keycloak UI is opened for the first time, enter the admin username and password to create the admin account
- After creating the admin user, click on the “Administration Console” link, or go to “http://localhost:8080/admin” to open the Keycloak admin UI

![https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/keycloak_admin_creds_setup.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/keycloak_admin_creds_setup.png)
## Realms in Keycloak
- Realms are like organizations or universes in Keycloak
- Multiple realms can be created and Clients, Users, Scopes, Resources of each realm can be managed in isolation
- For example, separate realms can be used to manage users of separate organizations
- By default, a realm named “master” is created

![https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/keycloak_master_realm.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/keycloak_master_realm.png)
- As a security best practice, always create the users and clients in a separate realm other than “master”
- A new realm can be created, or the displaying realm can be changed just by clicking the realm drop-down in the top-left as shown in the above image
- The Realm settings like default token expiration time, login screen customization etc., can be found in the “Realm Settings” section of the left navigation bar

## Managing Users, Clients, Scopes
- Keycloak provides a neat UI for managing the users, clients and client scopes
- Users can be managed by clicking the “Users” section of the left navigation bar
- Clients can be managed by clicking the “Clients” section of the left navigation bar
- Client Scopes can be managed by clicking the “Client Scopes” section of the left navigation bar

## Running in Production
* Keycloak servercan be setup very easily for development and testing purposes
* However this setup should not directly used in production
* A production ready database like PostgreSQL should be used instead of the default file based database
* SSL should be configured
* Proper logging should be configured
* A reverse proxy like IIS, apache2 or nginx should be used
* Further server administration guides can be found at https://www.keycloak.org/guides#server

## References
- Keycloak installation on bare metal - [https://www.keycloak.org/getting-started/getting-started-zip](https://www.keycloak.org/getting-started/getting-started-zip)
- OpenJDK download link - [https://jdk.java.net](https://jdk.java.net/)
- Keycloak zip download link - [https://www.keycloak.org/downloads](https://www.keycloak.org/downloads)

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY1Nzg3MTA0LDE4NTkzNjA0MjddfQ==
-->