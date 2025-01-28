# Reset PostgreSQL database password
If we forget the postgres user password of a PostgreSQL database, the following steps can be followed to reset the postgres user password

-   Access the database server console
-   Modify the pg_hba.conf file to trust localhost without password
-   Restart the database
-   Reset postgres user password with psql
-   Revert back the changes to pg_hba.conf file to enforce password authentication for localhost
-   Restart the database

## pg_hba.conf file location

-   pg_hba.conf file in windows is located in a folder location like `C:\\Program Files\\PostgreSQL\\[version]\\data`
-   pg_hba.conf file in Ubuntu is located in a folder location like `/etc/postgresql/[VERSION]/main/pg_hba.conf`

## Password-less database access for localhost

-   Ensure the following in pg_hba.conf file to allow password less database access for localhost (or 127.0.0.1/32)

```bash
# IPv4 local connections:
# TYPE  DATABASE        USER            ADDRESS                 METHOD
local    all             all             127.0.0.1/32            trust
```

-   Restart the database by restarting the PostgreSQL windows background service or by running `sudo systemctl restart postgresql` command in case of Ubuntu

## Reset postgres user password with psql

-   Connect to PostgreSQL database using the `psql` command line utility. In Ubuntu psql session to the database can be opened using the command `sudo -u postgres psql`
-   After opening the psql session, run the following SQL to reset the postgres user password

```sql
ALTER USER postgres with password 'new_secure_password'
```

## Enable password based access to localhost

-   Once the password reset activity is completed, it is safe to again enable password based database access for localhost
    
-   Revert back the database access setting for localhost (or 127.0.0.1/32) like the following to enable password based access
    
    ```bash
    # IPv4 local connections:
    # TYPE  DATABASE        USER            ADDRESS                 METHOD
    local    all             all             127.0.0.1/32            scram-sha-256
    
    ```
    
-   Restart the database again after changing the pg_hba.conf file. The configuration changes can also be applied by running the SQL command `SELECT pg_reload_conf();` in a psql session.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MzgyNjk0MTcsNzMwOTk4MTE2XX0=
-->