## Skill - Create API endpoints in flask 

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Extract parameters from URL in flask server](https://nagasudhir.blogspot.com/2022/04/extract-parameters-from-url-in-flask.html)


Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to create simple API endpoints in flask

## What is an API endpoint
* An api endpoint is just a URL at which the server listens for HTTP requests and send JSON or CSV or text as a response

### GET requests
```py
from flask import Flask

app = Flask(__name__)

# send json
@app.route('/hello_json')
def helloJson():
    return {'message': 'Hello World!!!'}

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=50100, debug=True)
```
* In the above example, the URL `localhost:50100` serves

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

### generate URLs to flask blueprint routes using "url_for"
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

### Video
The video for this post can be seen [here](https://youtu.be/SezbDCz0Ock)

<iframe width="560" height="315" src="https://www.youtube.com/embed/SezbDCz0Ock" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## References
* Official flask blueprints docs - https://flask.palletsprojects.com/en/latest/blueprints/

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM4MjAwMzQ4MywtMTYyMDA2ODU0Ml19
-->