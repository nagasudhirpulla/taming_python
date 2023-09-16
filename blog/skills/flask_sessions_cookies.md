## Sessions and cookies in flask

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)

Go through the above skills if necessary for reference or revision

<hr/>

## Why Cookies and Sessions

![http_is_stateless.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/http_is_stateless.png?raw=true)
-   HTTP protocol is stateless, i.e., each request does not have any context about the previous request
-   Cookies and sessions are used by the servers to store data across different pages of the website

## Cookie

![cookies_working.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/cookies_working.png?raw=true)
-   Cookies are set by the server and stored in the browser
-   Since Cookies are stored as plain text in the browser, they can be tampered by malicious actors
-   Cookie can be set by the server by adding the `Set-Cookie` header in the response. For example, the server can send a response header with cookie like `Set-Cookie: theme=dark` . This will set a cookie in the browser named `theme` with a value `dark` for the website
-   Once a cookie is set, it will be attached in the subsequent requests in the `Cookie` request header
-   The following example shows how to set cookie in a python flask server

### Cookie Flask example

```python
from flask import Flask, make_response

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello World!!!"

@app.route('/cookie')
def cookie():
    res = make_response("<h1>cookie is set</h1>")
    res.set_cookie('theme', 'dark')
    return res

if __name__ == '__main__':
    app.run(port=50100, debug=True)

```

## Session

![sessions_working.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/sessions_working.png?raw=true)
-   Sessions are used store data across requests at the server-side.
-   Sessions are more secure compared to cookies since data is stored in the server
-   Once a session is created, it will be assigned a unique id. This session id will be set as a cookie in the browser by the server. During the subsequent requests, the request session data will be retrieved by the server by looking up the session id
-   The following example shows how to create sessions in a python flask server

### Session Flask Example

```python
from flask import Flask, make_response, session
app = Flask(__name__)  
app.secret_key = "server_secret_string"  
 
@app.route('/')  
def home():  
    res = make_response("<h4>session variable is set, <a href='/get'>Get Variable</a></h4>")  
    session['username']='John'  
    return res;  
 
@app.route('/get')  
def getVariable():  
    if 'username' in session:  
        s = session['username'];  
        return f"User Name is {s}"  
  
if __name__ == '__main__':  
    app.run(port=50100, debug = True)

```

## Default Sessions Implementation in Flask

![flask_session_module_working.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/flask_session_module_working.png?raw=true)
-   Sessions are implemented as a signed cookies in flask. That means the whole session data is stored in the browser as a cookie.
-   However, the session cookie is signed cryptographically with the server secret key. So the server can easily detect if a session is tampered in the session cookie using the signature
-   Since the whole session data is visible in the browser cookie, secret and sensitive information should not be stored in flask sessions
-   The session data stored in the browser cookie would be in the format `<base64Encode(session_data)>.<UpdatedTime>.SHA1Hash(session_data, UpdatedTime, ServerSecret)` (Example: `eyJ1c2VybmFtZSI6IkpvaG4ifQ.ZQCnyw.pfqs2aFNJ7MNTdGyQi5E1xzlYzE`)

## Server-side sessions in flask using Flask-Session python module

-   Flask-Session python module can be used to implement server-side session storage instead of the default cookie based session storage
-   Only the session id will be present in the cookie. Session data will be present in the Flask server
-   Install flask-session python module using `python -m pip install Flask-Session`
-   Below example uses Flask-Session to implement server side sessions. The session data will be stored in a folder named _flask_session_ in the server

```python
from flask import Flask, session, make_response
from flask_session import Session

app = Flask(__name__)
app.config["SESSION_PERMANENT"] = False
app.config["SESSION_TYPE"] = "filesystem"
Session(app)

@app.route('/')
def home():
    res = make_response(
        "<h4>session variable is set, <a href='/get'>Get Variable</a></h4>")
    session['username'] = 'John'
    return res

@app.route('/get')
def getVariable():
    if 'username' in session:
        s = session.get("username")
        return f"User Name is {s}"

if __name__ == '__main__':
    app.run(port=50100, debug=True)

```

-   Other session storage approaches like redis, memcached, sqlalchemy, mongodb can also be used

### Video
The video for this post can be seen [here](https://youtu.be/Y4qHNcl4f0Y?si=d7KyaCcFxuLsllKd)

<iframe width="560" height="315" src="https://www.youtube.com/embed/G4Tng6666SI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## References

-   https://www.javatpoint.com/session-vs-cookies
-   Flask sessions docs - https://flask.palletsprojects.com/en/2.3.x/quickstart/#sessions
-   Flask cookies docs - https://flask.palletsprojects.com/en/2.3.x/quickstart/#cookies
-   Flask-Session module docs - https://flask-session.readthedocs.io/en/latest/quickstart.htm
-   https://blog.paradoxis.nl/defeating-flasks-session-management-65706ba9d3ce
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjE0MTYxODYzNSwtNjU2MTY2Nzc0LC03ND
AyMjI3MTNdfQ==
-->