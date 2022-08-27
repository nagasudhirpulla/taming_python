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
* In the above example, the URL to the flask route function `getItem` within the same blueprint can be generated using `url_for('.getItem')`. Hence relative URLs with in the same blueprint can be generated using the '.' notation.
* The URL for flask route function `list` within the blueprint `authors` can be generated using `url_for('authors.list')`

### static/styles/theme.css file
```css
/* static/styles/theme.css file */
body {
    color: rgb(201, 209, 217);
    background-color: rgb(13, 17, 23);
}

a {
    color: rgb(83, 189, 235);
}
```

## 'register_error_handler' method or 'errorhandler' decorator for custom error pages
```py
# server.py file
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template("home.html")

def genericErrorHandler(error):
    return render_template("message.html", title=error.name, message=error.description), error.code

for errCode in [400, 401, 403, 404]:
    app.register_error_handler(errCode, genericErrorHandler)


@app.errorhandler(500)
@app.errorhandler(501)
def serverError(error):
    return render_template("message.html", title="Internal Server Error", message="Some Internal Error occured..."), error.code


app.run(host="0.0.0.0", port=50100, debug=True)
```

* As shown in the above code, using the `app.register_error_handler` method or `errorhandler` decorator, we can render error page for a specific HTTP error codes
* The error handler function takes in an error object. Each error object contains `code`, `name`, `description` properties
* A template located at `templates/message.html` is rendered while handling the error

### templates/message.html file
```html
<!-- templates/message.html file -->
<!DOCTYPE html>
<html lang="en">

<head>
    <link rel="stylesheet" href="{{url_for('static', filename='styles/theme.css')}}">
    <title>{{ title }}</title>
</head>

<body>
    <h2>{{ title }}</h2>
    <h4>{{ message }}</h4>
    <a href="{{ url_for('index') }}">Click here</a> to go to Home page
</body>

</html>
```
* This is the template for our custom error page
* We are able to control the styling 
* Link to home page is also added 

## Default error handler for all HTTP errors
* Instead of explicitly specifying the error handler for each HTTP error code, we can define a default error handler for all HTTP exceptions as shown below

```py
# server.py file
from flask import Flask, render_template
from werkzeug.exceptions import HTTPException

app = Flask(__name__)

@app.route('/')
def index():
    return render_template("home.html")


@app.errorhandler(HTTPException)
def handleException(error):
    return render_template("message.html", title=error.name, message=error.description), error.code


@app.errorhandler(500)
def serverError(error):
    return render_template("message.html", title="Server Error", message="Oops, some error occured..."), error.code


app.run(host="0.0.0.0", port=50100, debug=True)
```

* In the above example, using the `@app.errorhandler(HTTPException)` decorator, all the HTTP errors are handled by the `handleException` method by default
* However for error code 500, since we have specifically mentioned a method with decorator `@app.errorhandler(500)`, the `serverError` method will be called for handling HTTP error with status code 500

## Simulate HTTP errors using 'abort' method
* To check the rendering of error pages, we can throw HTTP errors using the `abort` function from the flask module as shown below  

```py
from flask import Flask, abort, render_template
from werkzeug.exceptions import HTTPException

app = Flask(__name__)

@app.route('/')
def index():
    return render_template("home.html")


@app.route('/simulate500')
def simulate500():
    return abort(500)


@app.errorhandler(HTTPException)
def handleException(error):
    return render_template("message.html", title=error.name, message=error.description), error.code

app.run(host="0.0.0.0", port=50100, debug=True)
```
* In the above python server code, visiting the URL `/simulate500` will call the `abort(500)` method which throws the HTTP exception with status code 500

### Video
The video for this post can be seen [here](https://youtu.be/FlSDIqauUDY)

<iframe width="560" height="315" src="https://www.youtube.com/embed/FlSDIqauUDY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## References
* Official flask blueprints docs - https://flask.palletsprojects.com/en/latest/blueprints/

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNTA4NTM5MzksLTg3Nzg5NjQxNCwtMT
ExODM0MTM4NCwxNzIzMjE5NTEzLC0yMTQxNTg4Njc1LC0xMTIy
NzM3OTE5LC0xNDg1MzA5OTE3LC0xNTA2MjUyNjg5LDczMDk5OD
ExNl19
-->