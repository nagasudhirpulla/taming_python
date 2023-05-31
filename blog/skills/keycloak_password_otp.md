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
* Users can be managed from the "Users" tab of a keycloak realm as shown below
![users_tab_in_keycloak](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/users_tab_in_keycloak.png?raw=true)
- Password can be set in the "Credentials" tab of the user
![users_password_keycloak.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/users_password_keycloak.png?raw=true)
### Set Password Policy
- Password policy of a keycloak realm can be easily configured in the Authentication menu, Policies tab as shown below 
![password_policy_keycloak_setting.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/password_policy_keycloak_setting.png?raw=true)
- A variety of useful settings like password expiry days, recent passwords usage, password blacklist, minimum and maximum password length, minimum number of uppercase, lowercase and special characters can be specified easily in the password policy page
- Password blacklist file should be kept in the `data\password-blacklists\` folder of the keycloak folder. Also the password blacklist text file should have Unix style line endings (This needs to checked in windows)

### Enable and configure Two factor Authentication in Keycloak
-  By default two factor authentication is disabled in a Keycloak realm
- Two factor authentication can be enabled in the Authentication menu, Flows tab, browser flow as shown below  

![keycloak_otp_enable.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_otp_enable.png?raw=true)
- Two factor authentication policy can be configured from Authentication menu, Policies tab, OTP Policy tab as shown below

![keycloak_otp_enable.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_otp_policy.png?raw=true)
* OTP 

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
-   Official docs for password policy - https://www.keycloak.org/docs/latest/server_admin/#_password-policies

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExODkyNTc2MDAsLTg0OTYzMzgxLC0xMj
M1NjczODU1LC0xMDc2MjU1MDc4LDQxMzMzOTY3LC02NjQ3OTEw
MjYsMTExOTg3ODYwMCwtMjA3ODQ4NTk3MywxMTIzMjI3NTQ1XX
0=
-->