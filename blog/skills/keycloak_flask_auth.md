# Flask role-based authorization with Keycloak

The source code of the demo flask application can be found [here](https://github.com/nagasudhirpulla/flask_keycloak_auth)

## Why use Keycloak with Flask

-   Users database, login screen, user registration, two factor etc. are all implemented by Keycloak
-   Keycloak implements security best practices out of the box and can be configured easily using its admin portal
-   Flask application need not maintain a database to securely store user data
-   Single Sign On (SSO) can be implemented for multiple web applications with Keycloak since user logins are handled by Keycloak

## Workflow for authentication

![https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/Oauth Authorize Code flow.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/Oauth%20Authorize%20Code%20flow.png)

-   User clicks login button in the Flask application (client app)
-   Client application redirects the user to the Keycloak (OAuth server) authorization page to perform authentication. Information like callback URL is sent by the client application to OAuth server while redirecting the user.
-   After logging in the user, the OAuth server redirects the user to the callback URL of the client application along with additional information like authorization code.
-   Client application sends the authorization code, client id and client secret to the OAuth server for obtaining access token and id token
-   OAuth server validates the authorization code, client id and client secret and issues access token and id token to the client
-   Client application can access user information using `id_token` and call other APIs on behalf of the user using `access_token`
-   Client application can authenticate and login the user with the details in the `id_token` (like username, email etc.)

## Setup Keycloak (OAuth Server)

-   Login to Keycloak admin portal

### Create a realm

-   Create a realm for registering the flask application
-   Here we are creating a realm named **LearningSoftware**

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_flask_client/keycloak_create_realm.png?raw=true)

### Create a client for flask application

-   Register the Flask application in Keycloak by creating a client. The client Id and client secret will be used by the flask application.

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_flask_client/keycloak_flask_client_create1.png?raw=true)

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_flask_client/keycloak_flask_client_create2.png?raw=true)

![image (1).png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_flask_client/keycloak_flask_client_create3.png?raw=true)

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_flask_client/keycloak_flask_client_create4.png?raw=true)

### Create user roles used in the flask application

-   Goto the Roles tab of the client and create the roles used in the flask application

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_flask_client/keycloak_flask_client_roles.png?raw=true)

### Include user roles in user info endpoint and id token

-   Go to client scopes > roles > Mappers > client roles and enable “Add to ID token” and “Add to userinfo”

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_flask_client/keycloak_roles_in_token.png?raw=true)

### Create users in realm

-   Create user as shown below and also set password in the “Credentials” tab of the user

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_flask_client/keycloak_create_flask_user.png?raw=true)

### Assign roles to users

-   Open the user and go to the “Role mapping” tab to assign required roles to user as shown below

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_flask_client/keycloak_add_roles_to_flask_user.png?raw=true)

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_flask_client/keycloak_add_roles_to_flask_user2.png?raw=true)

## Create a Flask application (Client app)

### Authentication in Flask app with Keycloak

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_flask_client/keycloak_flask_auth_overview.png?raw=true)

### Role based authorization overview

-   Flask server fetches the id_token from Keycloak (OAuth server) upon the completion of user authentication
-   The id_token contains roles and user details (like username, email, user id)
-   This required user information along with user roles will be embedded in a flask session (implemented using cookies)
-   Whenever the user visits a web page, the roles are derived from the session and access will be granted if required user roles are present

### Keycloak config in Flask app

-   The client Id, client secret and realm discovery URL are required for the flask application as shown below

```json
{
    "oauthAppClientId": "flaskClient",
    "oauthAppClientSecret": "ST4rrbr4Z9sZSAhU9xkajfWYVcJEHnkx",
    "oauthProviderDiscoveryUrl": "http://localhost:8080/realms/LearningSoftware/.well-known/openid-configuration"
}

```

-   Client Id and client secret can be found taken by opening the credentials tab of the client
-   Realm discovery URL can be found in Keycloak in the Realm Settings page as shown below

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_flask_client/keycloak_realm_url_for_well_known.png?raw=true)

### Authorization decorator for flask route

-   For easy declaration of authorized user roles for flask routes, a python decorator as shown below can be used
-   The decorator checks the session if required user roles are present. If user is not logged in, it will redirect to the login page. If the user does not have required roles, it will throw an error with HTTP status code 401 (Unauthorized request)

```python
import functools
from flask import redirect, url_for, request, abort
from src.security.user import getUserFromSession

def login_required(_func=None, *, roles=[]):
    def decorator_login_required(func):
        """Make sure user is logged in before proceeding"""
        @functools.wraps(func)
        def wrapper_login_required(*args, **kwargs):
            user = getUserFromSession()
            if user == None:
                return redirect(url_for("oauth.login", next=request.url))
            # check user roles
            isRolesPresent = True if len(roles) == 0 else all(
                [rl in user["roles"] for rl in roles])
            if not isRolesPresent:
                return abort(401)
            return func(*args, **kwargs)
        return wrapper_login_required

    if _func is None:
        return decorator_login_required
    else:
        return decorator_login_required(_func)

```

### Using the authorization decorator on Flask routes

-   The decorator can used above flask route functions as shown below. If roles are mentioned, required user roles will be checked, otherwise logged in user will be granted access without checking roles

```python
@app.route('/profile')
@login_required
def profile():
    return render_template("profile.html")

@app.route('/admin')
@login_required(roles=["admin"])
def admin():
    return render_template("admin.html")

```

### User session operations

-   The functions shown below can be used to create user session, derive the logged in user from session and clear the user session
-   `id_token` (fetched from Keycloak during user login) is also stored in the user session since it is required for logging out the user from Keycloak during the logout process

```python
from flask import session
from typing import Optional, TypedDict

__sessionUserKey = 'user'

class User(TypedDict):
    userId: str
    userName: str
    email: str
    roles: list[str]
    idToken: str

def createUserSession(userId: str, userName: str, email: str, roles: list[str] = [], idToken=""):
    user: User = {
        "userId": userId,
        "userName": userName,
        "email": email,
        "roles": roles,
        "idToken": idToken
    }
    session[__sessionUserKey] = user

def clearUserSession():
    session.pop(__sessionUserKey, None)

def getUserFromSession() -> Optional[User]:
    if not __sessionUserKey in session:
        return None
    return session[__sessionUserKey]

```

### Flask Blueprint for Keycloak server interactions

-   All the flask server routes for Keycloak (OAuth server) interaction can be kept in a separate file using a flask blueprint as shown below

```python
from flask import Blueprint

oauthPage = Blueprint('oauth', __name__,
                      template_folder='templates')

oauth = None

@oauthPage.route("/login")
def login():
    # route for logging in the user
    ...

@oauthPage.route("/login/callback")
def callback():
    # route for OAuth server to send response after keycloak user authentication
    ...

@oauthPage.route("/logout")
def logout():
    # route for logging out the user from app as well as keycloak
    ...

```

### Authlib module for Keycloak interaction

-   Authlib python module can be used to easily implement OAuth 2.0 Authorization code flow in Flask applications. It can be installed with pip using `python -m pip install Authlib`
-   An instance of OAuth client can be created in a flask application as shown below

```python
from flask import current_app
from src.config.appConfig import getAppConfig
from authlib.integrations.flask_client import OAuth

oauth = None

def initOauthClient():
    global oauth
    appConfig = getAppConfig()
    oauth = OAuth(current_app)
    oauth.register(
        "keycloak",
        client_id=appConfig.oauthAppClientId,
        client_secret=appConfig.oauthAppClientSecret,
        client_kwargs={
            "scope": "openid profile email roles",
            # 'code_challenge_method': 'S256'  # enable PKCE
        },
        server_metadata_url=appConfig.oauthProviderDiscoveryUrl,
    )

```

### User login route

-   When user visits this page (/oauth/login), user will be redirected to Keycloak login page. The callback route URL will be provided to Keycloak via the URL query parameters while redirecting the user to Keycloak

```python
@oauthPage.route("/login")
def login():
    # check if session already present
    if "user" in session:
        abort(404)
    return oauth.keycloak.authorize_redirect(redirect_uri=url_for(".callback", _external=True))

```

### OAuth callback route

-   Keycloak sends authorization code to the flask application to a callback route. The URL to callback route will be provided to Keycloak via URL query parameter by flask application while redirecting the user to Keycloak login page
-   `oauth.keycloak.authorize_access_token()` gets the id token and access token from Keycloak by sending the client id, client secret and authorization code
-   User details along with roles are present in the id token itself (User details and roles can also be fetched from Keycloak using the user info endpoint with access token). User login is done by setting the user session with these fetched user details.

```python
@oauthPage.route("/login/callback")
def callback():
    tokenResponse = oauth.keycloak.authorize_access_token()
    idToken = tokenResponse["id_token"]
    userInfo = tokenResponse["userinfo"]
    # if roles are not included in id token, call user info endpoint explicitly 
    # userInfo = oauth.keycloak.userinfo()
    uRoles = userInfo['resource_access'][oauth.keycloak.client_id]["roles"]
    if not (isinstance(uRoles, list)):
        uRoles = [uRoles]
    createUserSession(
        userId=userInfo["sub"], userName=userInfo["preferred_username"], email=userInfo["email"], roles=uRoles, idToken=idToken)
    return redirect('/')

```

### User logout route

-   When user visits the page (/oauth/logout), the user is logged out from flask application by clearing the session
-   The user will be logged out from Keycloak also by calling the `end_session_endpoint` with id token

```python
@oauthPage.route("/logout")
def logout():
    # https://stackoverflow.com/a/72011979/2746323
    user = getUserFromSession()
    idToken = user["idToken"] if not user is None else None
    clearUserSession()
    if idToken:
        return redirect(str(oauth.keycloak.load_server_metadata().get('end_session_endpoint')) + "?"
                        + urlencode(
                            {
                                "post_logout_redirect_uri": url_for("index", _external=True),
                                "id_token_hint": idToken
                            },
                            quote_via=quote_plus))
    else:
        return redirect(url_for("index"))

```

### Checking if user is logged in in the jinja template

-   The session variable in the jinja template can be used to render user details or check if the user is logged in as shown below

```html
<!DOCTYPE html>
<html lang="en">
<body>
    {% if session['user'] %}
        <p>Hi, {{session['user']['userName']}}!</p>
        <a href="{{url_for('profile')}}">Profile</a><br>
        <a href="{{url_for('admin')}}">Admin Section</a><br>
        <a href="{{url_for('oauth.logout')}}">Logout</a><br>
    {% else %}
        <a href="{{url_for('oauth.login')}}">Login</a>
    {% endif %}
</body>
</html>

```

## Sessions implementation in Flask

-   Flask sessions are signed but not encrypted
-   Session data can be read from cookie
-   Encrypt session data separately if required

### Video
Video for this post can be found [here](https://youtu.be/AKTmvERQu20?si=_Hd5lIEBpuDMnrfs)

<iframe width="560" height="315" src="https://www.youtube.com/embed/AKTmvERQu20?si=_Hd5lIEBpuDMnrfs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## References

-   Authlib flask client documentation - [https://docs.authlib.org/en/latest/client/flask.html](https://docs.authlib.org/en/latest/client/flask.html)
-   [https://www.keycloak.org/securing-apps/oidc-layers](https://www.keycloak.org/securing-apps/oidc-layers)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzQ1OTM1Mjc3LDk3OTI4NTU3OCwtMTIxNj
IzNTk2Miw0NDA5NzQzNzYsLTgxNDA0OTg4MV19
-->