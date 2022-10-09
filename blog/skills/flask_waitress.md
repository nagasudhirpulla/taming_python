## Skill - Run a python Flask server with waitress as WSGI

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Sub mounting a flask application under a URL prefix](https://nagasudhir.blogspot.com/2022/08/sub-mounting-flask-application-under.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to use waitress as a WSGI (Web Server Gateway Interface) for a flask application

## Why use waitress
* The default flask server is not meant for production deployment since it is single-threaded and not highly secure
* Waitress is meant to be a production-quality pure-Python WSGI server with very acceptable performance

## What is Waitress
* Waitress is a pure python WSGI (Web Server Gateway Interface) server
* Waitress can run both on windows and Linux
* Waitress supports multi-threading and sub-mounting of application on a URL prefix
* Maximum number of parallel threads allowed can also be configured easily
* Waitress is often used along with reverse proxies like Nginx and IIS for production deployments

## Install waitress
* Waitress is just a python package
* It can be installed in a python environment using `pip`
```bat
python -m pip install waitress
```

## Example Flask server
The following is an example flask server that uses waitress as a WSGI
```py
from flask import Flask
from waitress import serve

app = Flask(__name__)

@app.route('/')
def index():
    return 'Hello, World with waitress!!!'

if __name__ == '__main__':
    serve(app, host='0.0.0.0', port=50100, threads=1)
```

### sub-mounting application on a URL prefix
* `url_prefix` option can be used in the `serve` function to sub-mount a flask application under a URL prefix
* This option is generally used with reverse proxies so that multiple applications can be hosted under multiple URL prefixes

```py
from flask import Flask
from waitress import serve

app = Flask(__name__)

@app.route('/hi')
def index():
    return 'Hello, World with waitress!!!'

if __name__ == '__main__':
    serve(app, host='0.0.0.0', port=50100, threads=1, url_prefix="/my-app")
```

### switch between waitress and default server based on development environment
```py
from flask import Flask
from waitress import serve

app = Flask(__name__)

@app.route('/')
def index():
    return 'Hello, World with waitress!!!'

mode = "dev"

if __name__ == '__main__':
    if mode == "dev":
        app.run(host='0.0.0.0', port=50100, debug=True)
    else:
        serve(app, host='0.0.0.0', port=50100, threads=1)

```

## References
* waitress documentation - https://docs.pylonsproject.org/projects/waitress/en/stable/index.html
* Flask quick-start guide - https://flask.palletsprojects.com/en/2.2.x/quickstart/

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NDg2MzAwNDYsLTYzMTUzNzE2OCw4OD
AxNzkxNSwxNTY5ODc2OTg5LDE0ODc2MTI5ODQsLTc0MDQxNzI5
NywtMTU2OTU3ODY2NSwtMTcxNzAyNjAzMyw3ODg3ODkzMDNdfQ
==
-->