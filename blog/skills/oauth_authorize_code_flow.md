## OAuth 2.0 Authorization Code flow for securing server side web applications

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
-   [OAuth 2.0 for centralized Authorization and Authentication of users and applications](https://nagasudhir.blogspot.com/2023/03/oauth-20-for-centralized-authorization.html)
- [Setup Keycloak as OAuth 2.0 server in Windows for testing and development](https://nagasudhir.blogspot.com/2023/04/setup-keycloak-as-oauth-20-server-in.html)

<br>

* In this post we will learn how can we secure server-side web applications with **OAuth 2.0 Authorization Code flow**

## Why use OAuth 2.0 Authorization Code flow
* The users information (name, email, roles etc.,) can be managed and stored securely in the OAuth server and need not be created separately in each web application
* The login screen, user account management, user administration pages are implemented by the OAuth server. Hence web applications can choose not to store users information in a database or implement login, account management and user administration pages.
* Since the users information is centrally stored in the OAuth server, multiple web applications can make users login with same credentials in a single login screen, thus facilitating Single-Sign-On (SSO)
* Web applications can be restricted to access only necessary user identity information from OAuth server
* Web application can call other APIs on behalf of the logged in user using the access token issued by the OAuth server while logging in the user

### Workflow of Authorization Code flow

![Oauth%20Authorize%20Code%20flow.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/Oauth%20Authorize%20Code%20flow.png)
### Client and user registration in OAuth server
- Client application will be registered in the OAuth server. The client will be given “client id” and “client secret” by the OAuth server
- Users will be registered in the OAuth server

### Steps
- User clicks login button in the client application
- Client application redirects the user to the OAuth server authorization page to perform authentication. Information like callback URL is sent by the client application to OAuth server while redirecting the user.
- After logging in the user, the OAuth server redirects the user to the callback URL of the client application along with additional information like authorization code.
- Client application sends the authorization code, client id and client secret to the OAuth server for obtaining access token and id token
- OAuth server validates the authorization code, client id and client secret and issues access token and id token to the client
- Client application can access user information using id_token and call other APIs on behalf of the user using access_token
- Client application can authenticate and login the user with the details present in the id_token (like username, email etc) 

## Authorization code flow demo with Keycloak



## References
- JWT decoder and verifier online - https://jwt.io
- purpose of nonce and state in authorization code flow - https://stackoverflow.com/a/48655220/2746323


<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMyODk3OTQ5NCw5OTY3ODc3MjUsMjE5Nj
A4NjAyLDEwOTMxODQ2MTYsLTEwMzEyNDk0MDAsLTM2OTI3Nzkx
MywtMzc1MDI2MDM1LC0xMzE0NjM4MzMsOTY1NjEzNTAwLDE4NT
AwNzM5MzIsLTE5NzYwMjY1NDldfQ==
-->