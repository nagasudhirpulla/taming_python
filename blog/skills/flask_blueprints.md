## Skill - Flask Blueprints for modular MVC like web applications

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Extract parameters from URL in flask server](https://nagasudhir.blogspot.com/2022/04/extract-parameters-from-url-in-flask.html)
* [jinja templates in flask](https://nagasudhir.blogspot.com/2022/04/jinja-templates-in-flask.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to use flask blueprints for creating modular MVC like web applications

## What is a Flask Blueprint
* A group multiple Flask routes can be segregated as a Flask Blueprint
* Each blueprint can be used like an MVC controller by registering each blueprint at a URL prefix
* Routes can be moved from the main server file into blueprints to reduce the lines of code 
* flask `url_for` function can be used to easily used to create relative URLs for a route within a blueprint or for a specific blueprint route

### Create a Flask Blueprint
The following python code serves a page `home.html` from the `templates` folder at the root URL. Also the `theme.css` is linked from the `static/styles` folder
```py
# src/controllers/books.py
from flask import Blueprint, render_template

booksCtrlr = Blueprint('books', __name__)

@booksCtrlr.route('/')
def list():
    return render_template("books/list.html")

@booksCtrlr.route('/<int:id>')
def getItem(id: int):
    return render_template("books/detail.html", id=id)
```
* A blueprint can be created from the `Blueprint` class imported from flask
* Functions can be declared as routes using annotations. For example, a route can be added to a blueprint named `booksCtrlr` using an annotation like `@booksCtrlr.route('/')`

### Add a blueprint to the flask application under a URL prefix
```py
# server.py
from flask import Flask, render_template
from src.controllers.books import booksCtrlr
from src.controllers.authors import authorsCtrlr

app = Flask(__name__)

@app.route('/')
def index():
    return render_template("home.html")

app.register_blueprint(booksCtrlr, url_prefix="/books")
app.register_blueprint(authorsCtrlr, url_prefix="/authors")

app.run(host="0.0.0.0", port=50100, debug=True)
```

* In the above example, the blueprint object is imported in the server file using `from src.controllers.books import booksCtrlr` 
* Then the blueprint is mounted to the main application named `app` at a prefix `/books` using `app.register_blueprint(booksCtrlr, url_prefix="/books")`

### dynamic URLs to flask blueprint routes using "url_for"
```html
<!-- templates/books/list.html file -->
<html>

<h2>List of Books</h2>
<ul>
    <li><a href="{{url_for('.getItem', id=1)}}">Item1</a></li>
</ul>

<a href="{{url_for('index')}}">Back to Home</a>
<br>
<a href="{{url_for('authors.list')}}">Authors</a>
</html>
```
* In the above example, the URL to the flask route function `getItem` within the same blueprint can be generated using `url_for('.getItem', id=1)`. Hence relative URLs with in the same blueprint can be generated using the '.' (dot) notation.
* The URL for flask route function `list` within the blueprint `authors` can be generated using `url_for('authors.list')`
* Hence URLs for routes inside blueprints can be generated using the '.' (dot) notation
* The  URL for the route function 'index' in the main server can be generated using `url_for('index')` 

## References
* Official flask blueprints docs - https://flask.palletsprojects.com/en/latest/blueprints/

<!--stackedit_data:
eyJoaXN0b3J5IjpbNzc4NTgyOTUyLDI3NTc4NTA2MywtMTE1MD
g1MzkzOSwtODc3ODk2NDE0LC0xMTE4MzQxMzg0LDE3MjMyMTk1
MTMsLTIxNDE1ODg2NzUsLTExMjI3Mzc5MTksLTE0ODUzMDk5MT
csLTE1MDYyNTI2ODksNzMwOTk4MTE2XX0=
-->