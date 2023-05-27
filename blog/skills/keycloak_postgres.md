## Skill - Setup PostgreSQL database for keycloak

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<br>

- In this post we will learn how to setup a PostgreSQL database for Keycloak and configure Keycloak to use that database
-   By default keycloak comes with a file based database to store the data like users, clients, credentials etc. on the disk
-   However in production scenarios, it is advisable to use a robust database like PostgreSQL database for storing the Keycloak data

### Setup PostgreSQL database to store Keycloak data
-   In Windows, the PostgreSQL command line session can be activated by running the psql application (it can be searched in the task bar). In Ubuntu, PostgreSQL command line session can be accessed by running the commands `sudo -i -u postgres` and then `psql`
-   Open PostgreSQL command prompt and run the commands to
    -   create a database
    -   create a database user
    -   grant permissions of the newly created user to the newly created database.

The following commands can run in the PostgreSQL command line session. A database named `keycloak` and a database user named `keycloak_user`

```sql
create database keycloak;
create user keycloak_user with password 'keycloak123';
grant all privileges on database keycloak to keycloak_user;

```

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

### References

-   https://www.keycloak.org/server/db
-   https://www.tutorialsbuddy.com/keycloak-postgresql-setup
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE0MTI2MjY3LC0xNDkzODY0MTA3XX0=
-->