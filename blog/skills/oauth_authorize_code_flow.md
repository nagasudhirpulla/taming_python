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

### Register a client and user in a keycloak realm
* Create a realm in keycloak named *myorg*
* Create a client with id "test_web_app" and note the client id and client secret for use in the client application. Modify the client settings to support authorization flow and specify the required inputs like home URL, redirect URL, post-logout redirect URL
![keycloak_web_client_administration.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/keycloak_web_client_administration.png)
* Create a user with username "test_user" and set a password under the credentials section
* Users can login and manage their account at "http://localhost:8080/realms/myorg/account"
![keycloak_user_admin_page.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/keycloak_user_admin_page.png)
### Step 1 - Click the login button to be redirected to the OAuth Login screen
* TODO login link image
* TODO login page
* Notice that the URL of the login page looks something like:
`http://localhost:8080/realms/myorg/protocol/openid-connect/auth?response_type=code&client_id=test_web_app&redirect_uri=http%3A%2F%2Flocalhost%3A3000%2Fcallback&scope=openid+profile+email&state=fmrXezEZQO6xCUDdJH4bbX7AW66gWm&nonce=lcnKjZAnpYSqldG6amqk`
* The URL parameters *response_type, client_id, redirect_uri, scope, state, nonce* are passed in the user login page URL by the client application while redirecting the user to the OAuth login screen. 
Using these URL parameters, the OAuth server will know the client application details and requirements while authenticating the user.
* The following is the explanation for each URL parameter
	* `response_type=code`, means an authorization code is expected upon user login
	* `client_id` is provided for OAuth server to identify the client application
	* `scope` is the scopes requested by the client application. All the requ  


## References
- JWT decoder and verifier online - https://jwt.io
- purpose of nonce and state in authorization code flow - https://stackoverflow.com/a/48655220/2746323


<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE1NTgyOTQzOCwtMjA2NDA0ODk5NCwtND
Y3ODMwMDA5LDI0MTc1NTI3NCwtMzI4OTc5NDk0LDk5Njc4Nzcy
NSwyMTk2MDg2MDIsMTA5MzE4NDYxNiwtMTAzMTI0OTQwMCwtMz
Y5Mjc3OTEzLC0zNzUwMjYwMzUsLTEzMTQ2MzgzMyw5NjU2MTM1
MDAsMTg1MDA3MzkzMiwtMTk3NjAyNjU0OV19
-->