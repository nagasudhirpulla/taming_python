## Manage Users, Password policy and Two factor authentication in keycloak

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<br>

#### Skills required
- [Installing and managing a PostgreSQL database](https://nagasudhir.blogspot.com/2021/12/installing-and-managing-postgresql.html)
- [Setup Keycloak as OAuth 2.0 server in Windows for testing and development](https://nagasudhir.blogspot.com/2023/04/setup-keycloak-as-oauth-20-server-in.html)

<hr>

- In this post we will learn how to setup Password policy and Two factor authentication in keycloak
-   By default two factor authentication is disabled and no password policy is configured in keycloak
-   Configuring a better password policy and two factor authentication helps in drastically improving the security of the user login process 

### Creating and managing users in keycloak
* Users can be managed from the "Users" tab of the keycloak realm as shown below
![users_tab_in_keycloak](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/users_tab_in_keycloak.png?raw=true)
![users_password_keycloak.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/users_password_keycloak.png?raw=true)

### Configure Keycloak to use the PostgreSQL database
-   After setting up the database, Keycloak needs to be configured to use the PostgreSQL database
-   The database configuration can be changed in the conf/keycloak.conf file. The following configuration can be used to configure PostgreSQL database

```bash
# Database

# The database vendor.
db=postgres
db-url-database=keycloak
db-url-host=localhost
db-url-port=5432

# Use jdbc url to specify the postgresql connection in one line instead of the above options
# db-url=jdbc:postgresql://localhost/keycloak

# The username of the database user.
db-username=keycloak_user

# The password of the database user.
db-password=keycloak123

# The full database JDBC URL. If not provided, a default URL is set based on the selected database vendor.
#db-url=jdbc:postgresql://localhost/keycloak

```

-   The above configuration specifies the database type, database name, database host and database host. Alternatively, a single JDBC connection string can also be used instead of these options to specify connection configuration in one line. All the possible database configuration options are documented at https://www.keycloak.org/server/db
-   After saving the configuration file, restart the Keycloak server. Then Keycloak should use the PostgreSQL database to store its data

### Video
You can see the video for this post [here](https://youtu.be/7404ir5oq4Q)

<iframe width="560" height="315" src="https://www.youtube.com/embed/7404ir5oq4Q" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

### References
-   https://www.keycloak.org/server/db
-   https://www.tutorialsbuddy.com/keycloak-postgresql-setup

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY2NDc5MTAyNiwxMTE5ODc4NjAwLC0yMD
c4NDg1OTczLDExMjMyMjc1NDVdfQ==
-->