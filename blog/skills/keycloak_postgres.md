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
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0OTM4NjQxMDddfQ==
-->