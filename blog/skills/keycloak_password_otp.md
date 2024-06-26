## Manage Users, Login screen, Password policy and Two factor authentication in keycloak

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
### User Login screen settings
* Forgot password, Remember me, Email verification, User registration can be enabled or disabled in the Reals Settings menu, Login tab as shown below. 

![keycloak_login_screen_settings.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_login_screen_settings.png?raw=true)
* But to send the emails from keycloak, the email server settings are to be configured in the Email tab of the realm settings as shown below. In case of gmail, use app password instead of the original account password. A blog on how to use Gmail App passwords can be fount at https://nagasudhir.blogspot.com/2022/01/send-email-with-attachments-in-python.html

![keycloak_email_settings.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_email_settings.png?raw=true)
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

![keycloak_otp_policy.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_otp_policy.png?raw=true)

### Using Two factor authentication by the users
* For Two factor authentication, users can use any one of the FreeOTP, Google Authenticator, Microsoft Authenticator apps. In this demo, we are using Microsoft Authenticator app.
* Since our realm name is 'myorg', go to the URL http://localhost:8080/realms/myorg/account for login screen.
* After logging in for the first time with password,  user will be shown a QR code to configure the Authenticator app as shown below

![keycloak_otp_qr_code_setup.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_otp_qr_code_setup.png?raw=true)
* The one time code can be entered using the authenticator app by adding a new account in the Authenticator app as shown below

![keycloak_microsoft_authenticator_steps.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_microsoft_authenticator_steps.png?raw=true)
* After completing the Two factor authentication setup with an Authenticator app, the user will be asked for an OTP to login as shown below

![keycloak_login_otp.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_login_otp.png?raw=true)

### Video
You can see the video for this post [here](https://youtu.be/rVC9JMGMU-w)

<iframe width="560" height="315" src="https://www.youtube.com/embed/rVC9JMGMU-w" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

### References
- Official docs for password policy - https://www.keycloak.org/docs/latest/server_admin/#_password-policies
- Official docs for OTP policy -https://www.keycloak.org/docs/latest/server_admin/#one-time-password-otp-policies
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTk1NDQ3MTIxLC0xMjk4Njg1NTEzLC0xMj
YxODA4ODUwLC0xODk4NjM1NDk4LDg4NDgzMTIyMSwtMzYyOTE2
NjIwLDExODg2NzgwMzIsLTEwNDQ4MzQ1MDIsLTg0OTYzMzgxLC
0xMjM1NjczODU1LC0xMDc2MjU1MDc4LDQxMzMzOTY3LC02NjQ3
OTEwMjYsMTExOTg3ODYwMCwtMjA3ODQ4NTk3MywxMTIzMjI3NT
Q1XX0=
-->