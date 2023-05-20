## Implement login with google in python flask applications

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
-   [OAuth 2.0 for centralized Authorization and Authentication of users and applications](https://nagasudhir.blogspot.com/2023/03/oauth-20-for-centralized-authorization.html)
- [Setup Keycloak as OAuth 2.0 server in Windows for testing and development](https://nagasudhir.blogspot.com/2023/04/setup-keycloak-as-oauth-20-server-in.html)
- [OAuth 2.0 Authorization Code flow for securing server side web applications](https://nagasudhir.blogspot.com/2023/04/oauth-20-authorization-code-flow-for.html)

<br>

* In this post we will learn how to implement login with google in flask applications
* Also we will fetch user's personal information like age and gender from google after the user logs in

### Why use Google Login
* One of the use case can be to easily sign up users by extracting data like name, profile picture, gender and date of birth from google
* Inm

### Workflow of Authorization Code flow

![Oauth%20Authorize%20Code%20flow.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/Oauth%20Authorize%20Code%20flow.png)
#### Client and user registration in OAuth server
- Client application will be registered in the OAuth server. The client will be given “client id” and “client secret” by the OAuth server
- Users will be registered in the OAuth server

#### Steps
- User clicks login button in the client application
- Client application redirects the user to the OAuth server authorization page to perform authentication. Information like callback URL is sent by the client application to OAuth server while redirecting the user.
- After logging in the user, the OAuth server redirects the user to the callback URL of the client application along with additional information like authorization code.
- Client application sends the authorization code, client id and client secret to the OAuth server for obtaining access token and id token
- OAuth server validates the authorization code, client id and client secret and issues access token and id token to the client
- Client application can access user information using id_token and call other APIs on behalf of the user using access_token
- Client application can authenticate and login the user with the details present in the id_token (like username, email etc) 

### Authorization code flow demo with Keycloak

#### Register a client and user in a keycloak realm
* Create a realm in keycloak named *myorg*
* Create a client with id "test_web_app" and note the client id and client secret for use in the client application. Modify the client settings to support authorization flow and specify the required inputs like home URL, redirect URL, post-logout redirect URL

![keycloak_client_authorization_code_settings.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/keycloak_client_authorization_code_settings.png)

* Create a user with username "test_user" and set a password under the credentials section
* Users can login and manage their account at "http://localhost:8080/realms/myorg/account"
![keycloak_user_admin_page.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/keycloak_user_admin_page.png)
#### Step 1 - Click the login button to be redirected to the OAuth Login screen
* We will use a flask web application as a client application to demonstrate the authorization code flow  

![oauth_authorization_code_flow_login_link.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/oauth_authorization_code_flow_login_link.png) 

![oauth_authorization_code_flow_login_screen.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/oauth_authorization_code_flow_login_screen.png)

* Notice that the URL of the login page looks something like:
`http://localhost:8080/realms/myorg/protocol/openid-connect/auth?response_type=code&client_id=test_web_app&redirect_uri=http%3A%2F%2Flocalhost%3A3000%2Fcallback&scope=openid+profile+email&state=XchdBv68AuOBJ1nEcJm4gGu2FqqNJd&nonce=QLKWRrW9aaSiZaKTEUMi`
* The URL parameters *response_type, client_id, redirect_uri, scope, state, nonce* are passed in the user login page URL by the client application while redirecting the user to the OAuth login screen. 
Using these URL parameters, the OAuth server will know the client application details and requirements while authenticating the user.
* The following is the explanation for each URL parameter
	* `response_type=code`, means an authorization code is expected upon user login
	* `client_id` is provided for OAuth server to identify the client application
	* `scope` is the scopes requested by the client application to be present in the access token. All the specified scopes should be configured in the OAuth server while registering the client application
	*  `redirect_uri` specifies the client application URL to redirect the user after successfully logging in into the OAuth server. The redirect URL should be configured in the OAuth server while registering the client under the section "Valid redirect URIs"
	* `state` is a string passed in the request by client application to the OAuth server. OAuth server should respond with this `state` along with authorization code to prove that the response sent corresponds to that request only
	* `nonce` is a string passed in the request by client application to OAuth server. OAuth server should provide this nonce in the id token issued to the client application to prove that the id token corresponds to that request only
* Both the `state` and `nonce` are used to ensure that the communication between client application and OAuth server is not hijacked by malicious actors 

#### Step 2 - OAuth server sends Authorization code to client application 
* After the user logs in the OAuth server redirects the user to the client application's redirect URL as shown below
`http://localhost:3000/callback?state=XchdBv68AuOBJ1nEcJm4gGu2FqqNJd&session_state=3d3e12f0-f19c-4cf1-a39d-71ac90236c76&code=44f2e080-f5ea-4331-a762-2e3de3aef67f.3d3e12f0-f19c-4cf1-a39d-71ac90236c76.bc451cba-2043-447f-afc7-5176e2331517`
* The URL parameters `state, session_state, code` are added in the redirection URL. These URL parameters are the response from the OAuth server
* The following is the explanation for each URL parameter
	* `code` is the authorization code received from the OAuth server after authenticating the user. This will used by the client application to request the access token and id token from OAuth server. 
	* `state` is the string passed by the client application while requesting authorization code. This will matched by the client application for validating the response
	*  `session_state` is the session identifier maintained by the OAuth server for the ongoing login process. This needs to be sent by the client application while requesting access token and id token from OAuth server

#### Step 3 - Client application gets the access token and ID token from OAuth server
* After getting the authorization code from OAuth server, the client application sends a request to OAuth server for access token and id token.
* In our example, a POST request is sent by client application to the OAuth server's token endpoint URL as shown below
```
POST /realms/myorg/protocol/openid-connect/token HTTP/1.1
Host: localhost:8080
User-Agent: Authlib/1.2.0 (+https://authlib.org/)
Accept-Encoding: gzip, deflate
Accept: application/json
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded;charset=UTF-8
Content-Length: 199
Authorization: Basic dGVzdF93ZWJfYXBwOm1paVlMWWFEVDcya2pjZkRQTjFPWWo4a0hzOHJEZzNT

grant_type=authorization_code&redirect_uri=http%3A%2F%2Flocalhost%3A3000%2Fcallback&code=44f2e080-f5ea-4331-a762-2e3de3aef67f.3d3e12f0-f19c-4cf1-a39d-71ac90236c76.bc451cba-2043-447f-afc7-5176e2331517
```

* The client id and client secret are sent as base 64 encoded string (the format is "Basic base64encode(client_id:client_secret)") in the POST request's authorization header
* The POST request body contains the parameters `grant_type, code, redirect_uri`  
	* `grant_type=authorization_code` specifies the authorization flow
	* `code` is the authorization code received by the client application 
	* `redirect_uri` specifies the URL to which the authorization code was provided by the OAuth server
* The OAuth server validates the authorization code, client id and client secret and response with the id token and access token as shown below

```json
{
  "access_token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJXRld6eEtBNG9lN3FpNFpJUnNzN25hcEZrMXVianV2Z0NBZHp1MV92TktNIn0.eyJleHAiOjE2ODIxNjg1ODYsImlhdCI6MTY4MjE2ODI4NiwiYXV0aF90aW1lIjoxNjgyMTY4Mjg0LCJqdGkiOiJkYmNkMGNhMy00NzU1LTRhYmUtODY4My1iYzY3NzViNDUzNTIiLCJpc3MiOiJodHRwOi8vbG9jYWxob3N0OjgwODAvcmVhbG1zL215b3JnIiwiYXVkIjoiYWNjb3VudCIsInN1YiI6IjM1Y2RlYjY3LTk5ZWUtNGQwYS1iNzhiLThlOWM5YjYxMzllMCIsInR5cCI6IkJlYXJlciIsImF6cCI6InRlc3Rfd2ViX2FwcCIsIm5vbmNlIjoiUUxLV1JyVzlhYVNpWmFLVEVVTWkiLCJzZXNzaW9uX3N0YXRlIjoiM2QzZTEyZjAtZjE5Yy00Y2YxLWEzOWQtNzFhYzkwMjM2Yzc2IiwiYWNyIjoiMSIsImFsbG93ZWQtb3JpZ2lucyI6WyIiXSwicmVhbG1fYWNjZXNzIjp7InJvbGVzIjpbIm9mZmxpbmVfYWNjZXNzIiwiZGVmYXVsdC1yb2xlcy1teW9yZyIsInVtYV9hdXRob3JpemF0aW9uIl19LCJyZXNvdXJjZV9hY2Nlc3MiOnsiYWNjb3VudCI6eyJyb2xlcyI6WyJtYW5hZ2UtYWNjb3VudCIsIm1hbmFnZS1hY2NvdW50LWxpbmtzIiwidmlldy1wcm9maWxlIl19fSwic2NvcGUiOiJvcGVuaWQgcHJvZmlsZSBlbWFpbCIsInNpZCI6IjNkM2UxMmYwLWYxOWMtNGNmMS1hMzlkLTcxYWM5MDIzNmM3NiIsImVtYWlsX3ZlcmlmaWVkIjpmYWxzZSwibmFtZSI6IlRlc3QgVXNlciIsInByZWZlcnJlZF91c2VybmFtZSI6InRlc3RfdXNlciIsImdpdmVuX25hbWUiOiJUZXN0IiwiZmFtaWx5X25hbWUiOiJVc2VyIn0.JdIpJRdbfPk_8sFETZ79cPxl1a6yMZkylAPfUXlLF4kjsEiW9aEY5jp8dCLlkB_mOZ6T_pdR276m9hup7nPgGZv64YsZWcxoQpIbHr5PfX8maUOFoRaNdLCf4OoVwoZ2flIcGUIquHRW_6uzATtLYkEOLNvbIdfcPUCneFSEjnXXonTv8Ysm1X6qZmw_DUsX0kNRlfI3aObbzx2zPTQrD1SdTvb1riwgNabGxdh__47cjnG2-DxfXJOI7huug_JQL-P18lmEcXkCUdob41AYqDwIo8NndFlYMum2URBJAzS8CWdPx1WBa7P0UqAXuyzukmafzH4WHe2lwzKK-0jxdQ",
  "expires_in": 300,
  "refresh_expires_in": 1800,
  "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJkMzQ3NmEwYy1jMmRkLTRkZWItOWM2MC0xMjAxYTA1MzE4ZTMifQ.eyJleHAiOjE2ODIxNzAwODYsImlhdCI6MTY4MjE2ODI4NiwianRpIjoiYTdkZTRmNWMtM2E5YS00NTZlLTkyMDctMmI0NTkyMGQ4NmFhIiwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo4MDgwL3JlYWxtcy9teW9yZyIsImF1ZCI6Imh0dHA6Ly9sb2NhbGhvc3Q6ODA4MC9yZWFsbXMvbXlvcmciLCJzdWIiOiIzNWNkZWI2Ny05OWVlLTRkMGEtYjc4Yi04ZTljOWI2MTM5ZTAiLCJ0eXAiOiJSZWZyZXNoIiwiYXpwIjoidGVzdF93ZWJfYXBwIiwibm9uY2UiOiJRTEtXUnJXOWFhU2laYUtURVVNaSIsInNlc3Npb25fc3RhdGUiOiIzZDNlMTJmMC1mMTljLTRjZjEtYTM5ZC03MWFjOTAyMzZjNzYiLCJzY29wZSI6Im9wZW5pZCBwcm9maWxlIGVtYWlsIiwic2lkIjoiM2QzZTEyZjAtZjE5Yy00Y2YxLWEzOWQtNzFhYzkwMjM2Yzc2In0._mOhrVnAn-nS4FzMirFEOz7b9E1y-mVDowdWFGhsBQg",
  "token_type": "Bearer",
  "id_token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJXRld6eEtBNG9lN3FpNFpJUnNzN25hcEZrMXVianV2Z0NBZHp1MV92TktNIn0.eyJleHAiOjE2ODIxNjg1ODYsImlhdCI6MTY4MjE2ODI4NiwiYXV0aF90aW1lIjoxNjgyMTY4Mjg0LCJqdGkiOiI4ZjE5ZGQyYS01NWQwLTRiZDEtODAyZi04NjVhNDVlNmZiYjAiLCJpc3MiOiJodHRwOi8vbG9jYWxob3N0OjgwODAvcmVhbG1zL215b3JnIiwiYXVkIjoidGVzdF93ZWJfYXBwIiwic3ViIjoiMzVjZGViNjctOTllZS00ZDBhLWI3OGItOGU5YzliNjEzOWUwIiwidHlwIjoiSUQiLCJhenAiOiJ0ZXN0X3dlYl9hcHAiLCJub25jZSI6IlFMS1dSclc5YWFTaVphS1RFVU1pIiwic2Vzc2lvbl9zdGF0ZSI6IjNkM2UxMmYwLWYxOWMtNGNmMS1hMzlkLTcxYWM5MDIzNmM3NiIsImF0X2hhc2giOiJLdXdhQjdkVzhjQmczMzM1cTRXUFJRIiwiYWNyIjoiMSIsInNpZCI6IjNkM2UxMmYwLWYxOWMtNGNmMS1hMzlkLTcxYWM5MDIzNmM3NiIsImVtYWlsX3ZlcmlmaWVkIjpmYWxzZSwibmFtZSI6IlRlc3QgVXNlciIsInByZWZlcnJlZF91c2VybmFtZSI6InRlc3RfdXNlciIsImdpdmVuX25hbWUiOiJUZXN0IiwiZmFtaWx5X25hbWUiOiJVc2VyIn0.WxHzAAOFGrMPea6I1FVyaxFL4o-NxcM-ygynv_9WlfrkazLbq9QzcEOgsI8oSOXDQdslg5CHFRmJQRZJ0yu4SOpCHwyLUv-i84suvH_tU1iO4WfWQ1XhE79silUcwSzNE-rS-VRVaJ7oT4IF3I73k8A4XiwA2Ta5DEm4olmXGt4SVvYxm9TT_nvCjiwfnt6z1UpuigvQDGM_ANuthrdZjNnP-Sd57BihmvUYIt9UG8PrwKg0glHtTw7gDLiLz5UbHxcM5eShXYiRJBawb_ZV758F-_yH1REA7EcPtbWc76LE4dqe4F5ngg5RasohgMplL7Vhf84eGCgS0-Yf-PwIrQ",
  "not-before-policy": 0,
  "session_state": "3d3e12f0-f19c-4cf1-a39d-71ac90236c76",
  "scope": "openid profile email"
}
```

#### Step 4 - Client application parses the id token and authenticates user
* The id token returned by the OAuth server is a JWT that contains the user information in the JWT payload as shown below

```json
{
  "exp": 1682168586,
  "iat": 1682168286,
  "auth_time": 1682168284,
  "jti": "8f19dd2a-55d0-4bd1-802f-865a45e6fbb0",
  "iss": "http://localhost:8080/realms/myorg",
  "aud": "test_web_app",
  "sub": "35cdeb67-99ee-4d0a-b78b-8e9c9b6139e0",
  "typ": "ID",
  "azp": "test_web_app",
  "nonce": "QLKWRrW9aaSiZaKTEUMi",
  "session_state": "3d3e12f0-f19c-4cf1-a39d-71ac90236c76",
  "at_hash": "KuwaB7dW8cBg3335q4WPRQ",
  "acr": "1",
  "sid": "3d3e12f0-f19c-4cf1-a39d-71ac90236c76",
  "email_verified": false,
  "name": "Test User",
  "preferred_username": "test_user",
  "given_name": "Test",
  "family_name": "User"
}
```

* Since the id token is a JWT, token the integrity can also be checked by client application using the OAuth server public key
* The user information from the id token can be used by the client application to create a user session

![oauth_authorization_code_login_complete_page.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/oauth_authorization_code_login_complete_page.png)
#### Logging out the user
* Just clearing the user session in the client application will not log out the user from the OAuth server
* So after clearing the user session in the client application, the user will be redirected the logout endpoint URL (for example, http://localhost:8080/realms/myorg/protocol/openid-connect/logout) of the OAuth server. The URL will have the id_token and post logout redirect URL as the query parameters.
* After the logging out the user, the OAuth server will redirect the user to the post logout redirect URL of the client application

### Client application implementation in python flask
* All the OAuth 2.0 workflow is implemented in the server using the `authlib` module
* Ensure flask, authlib and requests modules are installed using the command `python -m pip install flask authlib requests`
* The server uses flask session to create a user login session in the flask application after successful user login at the OAuth server

```py
"""Python Flask WebApp OAuth 2.0 Authorization code flow example
"""

import json
from urllib.parse import quote_plus, urlencode

from authlib.integrations.flask_client import OAuth
from flask import Flask, abort, redirect, render_template, session, url_for

appConf = {
    "OAUTH2_CLIENT_ID": "test_web_app",
    "OAUTH2_CLIENT_SECRET": "miiYLYaDT72kjcfDPN1OYj8kHs8rDg3S",
    "OAUTH2_ISSUER": "http://localhost:8080/realms/myorg",
    "FLASK_SECRET": "ALongRandomlyGeneratedString",
    "FLASK_PORT": 3000
}

app = Flask(__name__)
app.secret_key = appConf.get("FLASK_SECRET")

oauth = OAuth(app)
oauth.register(
    "myApp",
    client_id=appConf.get("OAUTH2_CLIENT_ID"),
    client_secret=appConf.get("OAUTH2_CLIENT_SECRET"),
    client_kwargs={
        "scope": "openid profile email",
        # 'code_challenge_method': 'S256'  # enable PKCE
    },
    server_metadata_url=f'{appConf.get("OAUTH2_ISSUER")}/.well-known/openid-configuration',
)


@app.route("/")
def home():
    return render_template(
        "home.html",
        session=session.get("user"),
        pretty=json.dumps(session.get("user"), indent=4),
    )


@app.route("/callback")
def callback():
    token = oauth.myApp.authorize_access_token()
    session["user"] = token
    return redirect(url_for("home"))


@app.route("/login")
def login():
    # check if session already present
    if "user" in session:
        abort(404)
    return oauth.myApp.authorize_redirect(redirect_uri=url_for("callback", _external=True))


@app.route("/loggedout")
def loggedOut():
    # check if session already present
    if "user" in session:
        abort(404)
    return redirect(url_for("home"))


@app.route("/logout")
def logout():
    # https://stackoverflow.com/a/72011979/2746323
    id_token = session["user"]["id_token"]
    session.clear()
    return redirect(
        appConf.get("OAUTH2_ISSUER")
        + "/protocol/openid-connect/logout?"
        + urlencode(
            {
                "post_logout_redirect_uri": url_for("loggedOut", _external=True),
                "id_token_hint": id_token
            },
            quote_via=quote_plus,
        )
    )


if __name__ == "__main__":
    app.run(host="0.0.0.0", port=appConf.get("FLASK_PORT", 3000), debug=True)

```

```html
<!-- templates/home.html file-->
<html>

<head>
    <meta charset="utf-8" />
    <title>Authorization Code Flow Flask Example Web app</title>
</head>

<body>
    {% if session %}
    <h1>Welcome {{session.userinfo.name}}!</h1>
    <p><a href="/logout">Logout</a></p>
    <div><pre>{{pretty}}</pre></div>
    {% else %}
    <h1>Welcome Guest</h1>
    <p><a href="/login">Login</a></p>
    {% endif %}
</body>

</html>
```

* The user login URL is implemented in the ***/login*** route of the flask server. The  `authorize_redirect` function will create the login URL and redirect the user to the login page of the OAuth server
* The login redirect endpoint is implemented in ***/callback*** route of the flask server. The `authorize_access_token` function will fetch and validate the access token and id token using the authorization code sent from the OAuth server
* The logout URL is implemented in the ***/logout*** route of the flask server. The client application user session is cleared and the user is redirected to the OAuth server logout URL for logging out from the OAuth server also
* The post logout redirect URL is implemented in the ***/loggedout*** route of the flask server. After logging out the user, the OAuth server will redirect the user to this URL of the client application
* In this flask server, flask session is used for managing the user session. Other approaches for managing user sessions like using ***flask-login*** can also be adopted.

### PKCE in OAuth 2.0 Authorization code flow

* Proof Key for Code Exchange (PKCE) adds additional security while exchanging authorization code between client and OAuth server
* A random string (called code verifier) is generated and the hash of it (called code challenge) is sent along the login request to OAuth server
* After successful login by the user and receiving authorization code by client, the client sends the code verifier along with the client credentials in the token request. The OAuth server validates the token request by verifying the code challenge and code verifier
* By adopting PKCE, even if the authorization code is sniffed by the malicious parties, they cannot impersonate the client since the code verifier does not leave the client till the token request
* PKCE can be added in a python OAuth client just by adding `'code_challenge_method': 'S256'` in the client_kwargs while using the authlib module

  
![OAuth authorization code flow with PKCE workflow](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/oauth%20authorization%20code%20flow%20with%20pkce%20workflow.png?raw=true)

### Video
You can see the video on this post [here](https://youtu.be/K7aC4nZEepk) and [here](https://youtu.be/O065sJQs51U)

<iframe width="560" height="315" src="https://www.youtube.com/embed/K7aC4nZEepk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/O065sJQs51U" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

### References
- JWT decoder and verifier online - https://jwt.io
- purpose of nonce and state in authorization code flow - https://stackoverflow.com/a/48655220/2746323


<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgyOTEzOTAyNCwyMTM5MDczOTc0XX0=
-->