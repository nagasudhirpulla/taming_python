## Implement login with google in python flask applications

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
-   [OAuth 2.0 for centralized Authorization and Authentication of users and applications](https://nagasudhir.blogspot.com/2023/03/oauth-20-for-centralized-authorization.html)
- [Setup Keycloak as OAuth 2.0 server in Windows for testing and development](https://nagasudhir.blogspot.com/2023/04/setup-keycloak-as-oauth-20-server-in.html)
- [OAuth 2.0 Authorization Code flow for securing server side web applications](https://nagasudhir.blogspot.com/2023/04/oauth-20-authorization-code-flow-for.html)

<hr>

* In this post we will learn how to implement login with google in flask applications
* Also we will fetch user's personal information like age and gender from google after the user logs in

### Why use Google Login
* One of the use case can be to easily sign up users by extracting data like name, profile picture, gender and date of birth from google
* For locally hosted flask applications or simple flask applications, implementing robust security is more difficult than the application itself. Maintaining the users information securely, implementing the login and logout screens with robust security is difficult in flask applications. For such scenarios, the server can have a list of allowed gmail emails and make the users to login using google. This makes the login implementation very simple and highly secure

### How google login works
* Google supports OAuth 2.0 Authorization code flow for logging in users from external applications like the flask application in our example
* OAuth 2.0 Authorization code flow is a workflow for delegated  authorization where the OAuth server issues tokens to external applications for accessing user data after the user logs in
* The following is the workflow of Authorization Code flow
	* User clicks the login button and will be redirected to google login screen by our flask application. The login url will also contains additional required parameters like client id, client secret, scopes, callback URL
	*  After the user logs in, the user will be redirected to our flask application callback URL with the authorization code in the request URL
	* Our flask application will use the authorization code to fetch the id toke and access token from google
	* After fetching the id token and access token, the user's birthday and gender will be accessed by calling the Google People API with the access token attached to the request
	* The user will now be logged into our flask application by creating a flask session

![Oauth%20Authorize%20Code%20flow.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/Oauth%20Authorize%20Code%20flow.png)
### Registering the flask application in Google Developer Console
The following is the procedure to register our flask application and obtain the client id and client secret from Google Developer Console: 
- Open Google Developer Console
- Click on "Create Project" and create a project
- Go to the project and click "APIs & Services" in the left navigation bar
- Click on the "Enabled APIs & Services" menu in the left navigation bar and click the "ENABLE APIs AND SERVICES" button. Since we want to access the user's birthday and gender, we need to enable the "Google People API"
-  Go to the project and click "OAuth consent screen" in the left navigation bar. Setup the consent screen by filling in the required details. Set the Publishing status to Production instead of testing. In testing mode, only selected emails can login. In Production mode, any Gmail email can login. Select the email, profile, openid, gender and birthday scopes 
- Go to the project and click on "Credentials" in the left menu. Click on "CREATE CREDENTIALS" button at the top. Select OAuth Client ID. Select the application type as Web application and provide a name and an "Authorized redirect URIs". In our example the "Authorized redirect URI" is "http://localhost:5000/signin-google"
- Authorized redirect URI is the URL the user will be redirected to after successful login
- After creating the credentials the client id and client secret are displayed on the screen. These are required in the flask application


![google_oauth_web_app_credentials.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/google_oauth_web_app_credentials.png)<br>
<br>

![google_oauth_web_app_credentials_settings.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/google_oauth_web_app_credentials_settings.png)

#### Logging out the user
* When user clicks the logout button, the flask user session will be cleared at the server, resulting in logging out the user

### Flask server python Code
* All the OAuth 2.0 workflow is implemented in the server using the `authlib` module
* Ensure flask, authlib and requests modules are installed using the command `python -m pip install flask authlib requests`
* The server uses flask session to create a user login session in the flask application after successful user login at the Google server
* In this python server code, an instance of OAuth app is initialized using authlib and the login, callback and logout endpoints are implemented. The user is redirected in the login endpoint and the user information and tokens are fetched in the callback endpoint. 
* The user login session is created in the callback endpoint. 
* The user information and tokens are displayed in the home page after logging in by injecting session data into the jinja template by the server

```py
# server.py
import json

import requests
from authlib.integrations.flask_client import OAuth
from flask import Flask, abort, redirect, render_template, session, url_for

app = Flask(__name__)

appConf = {
    "OAUTH2_CLIENT_ID": "paste_client_id_here",
    "OAUTH2_CLIENT_SECRET": "paste_client_secret_here",
    "OAUTH2_META_URL": "https://accounts.google.com/.well-known/openid-configuration",
    "FLASK_SECRET": "ALongRandomlyGeneratedString",
    "FLASK_PORT": 5000
}

app.secret_key = appConf.get("FLASK_SECRET")

oauth = OAuth(app)
# list of google scopes - https://developers.google.com/identity/protocols/oauth2/scopes
oauth.register(
    "myApp",
    client_id=appConf.get("OAUTH2_CLIENT_ID"),
    client_secret=appConf.get("OAUTH2_CLIENT_SECRET"),
    client_kwargs={
        "scope": "openid profile email https://www.googleapis.com/auth/user.birthday.read https://www.googleapis.com/auth/user.gender.read",
        # 'code_challenge_method': 'S256'  # enable PKCE
    },
    server_metadata_url=f'{appConf.get("OAUTH2_META_URL")}',
)


@app.route("/")
def home():
    return render_template("home.html", session=session.get("user"),
                           pretty=json.dumps(session.get("user"), indent=4))


@app.route("/signin-google")
def googleCallback():
    # fetch access token and id token using authorization code
    token = oauth.myApp.authorize_access_token()

    # google people API - https://developers.google.com/people/api/rest/v1/people/get
    # Google OAuth 2.0 playground - https://developers.google.com/oauthplayground
    # make sure you enable the Google People API in the Google Developers console under "Enabled APIs & services" section

    # fetch user data with access token
    personDataUrl = "https://people.googleapis.com/v1/people/me?personFields=genders,birthdays"
    personData = requests.get(personDataUrl, headers={
        "Authorization": f"Bearer {token['access_token']}"
    }).json()
    token["personData"] = personData
    # set complete user information in the session
    session["user"] = token
    return redirect(url_for("home"))


@app.route("/google-login")
def googleLogin():
    if "user" in session:
        abort(404)
    return oauth.myApp.authorize_redirect(redirect_uri=url_for("googleCallback", _external=True))


@app.route("/logout")
def logout():
    session.pop("user", None)
    return redirect(url_for("home"))


if __name__ == "__main__":
    app.run(host="0.0.0.0", port=appConf.get(
        "FLASK_PORT"), debug=True)

```

```html
<!-- templates/home.html file-->
<html>

<head>
    <meta charset="utf-8" />
    <title>Flask Google Login Example Web Application</title>
</head>

<body>
    {% if session %}
    <h1>Welcome {{session.userinfo.preferred_username}}!</h1>
    <p><a href="{{url_for('logout')}}">Logout</a></p>
    <div><pre>{{pretty}}</pre></div>
    {% else %}
    <p><a href="{{url_for('googleLogin')}}">Login with Google</a></p>
    {% endif %}
</body>

</html>
```

### Video
The video for this post can be seen [here](https://youtu.be/fZLWO3_V06Q)

<iframe width="560" height="315" src="https://www.youtube.com/embed/fZLWO3_V06Q" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


### References
- Google developer console - https://console.cloud.google.com/
- List of google scopes - [](https://developers.google.com/identity/protocols/oauth2/scopes)[https://developers.google.com/identity/protocols/oauth2/scopes](https://developers.google.com/identity/protocols/oauth2/scopes)
- Google People API documentation - [](https://developers.google.com/people/api/rest/v1/people/get)[https://developers.google.com/people/api/rest/v1/people/get](https://developers.google.com/people/api/rest/v1/people/get)
- Google OAuth 2.0 playground - [](https://developers.google.com/oauthplayground)[https://developers.google.com/oauthplayground](https://developers.google.com/oauthplayground)


<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY0MzU0MzYzMSwtMTI1ODY5MjIyOSwyNj
g2OTQwMjksLTQyMjkyMzU0LC0xNjM2NTg4NjY1LC0xNDU3NTcy
MTcxLDEwNzc5MDE0MTMsLTU5Njc5ODE1OCw2MTUzMzAwOTQsLT
E5NzkwNTgyMTksMjEzOTA3Mzk3NF19
-->