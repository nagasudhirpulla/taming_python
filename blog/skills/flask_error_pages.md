## Skill - Custom Error Pages in python Flask application

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Serve static files in flask](https://nagasudhir.blogspot.com/2022/04/serve-static-files-in-flask.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to create custom error pages in a flask application and simulate errors in flask application

## Use cases
We can serve custom error pages for
* Providing additional content in the error pages like links to other pages etc
*  Custom styling of error pages

## Sample Server setup
The following python code serves a page `home.html` from the `templates` folder at the root URL. Also the `theme.css` is linked from the `static/styles` folder
```py
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template("home.html")

app.run(host="0.0.0.0", port=50100, debug=True)
```

### templates/home.html file
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <link rel="stylesheet" href="{{url_for('static', filename='styles/theme.css')}}">
    <title>Home</title>
</head>

<body>
    <h2>Hello World!!!</h2>
</body>

</html>
```

### static/styles/theme.css file
```css
body {
    color: rgb(201, 209, 217);
    background-color: rgb(13, 17, 23);
}

a {
    color: rgb(83, 189, 235);
}
```

## "register_error_handler" method or "error_handler" decorator for custom error pages
```py
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

* As shown in the above code, using the `app.register_error_handler` method or `errorhandler` decorator, we can render error page for a specific error codes
* The error handler function takes in an error object. Each error object contains `code`, `name`, `description` properties
* A page located at `templates/message.html` is rendered while handling the error

### templates/message.html file
```html
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
* We are able to control the styling and also link to home page is added 

### Default error handler for all HTTP errors
* Instead of explicitly specifying the error handler for each HTTP error code, we can define a default error handler for all HTTP exceptions as shown below

```py
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

### Video
The video for this post can be seen [here](https://youtu.be/_JiJGFAW43s)

<iframe width="560" height="315" src="https://www.youtube.com/embed/_JiJGFAW43s" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* Official flask error handling guide - https://flask.palletsprojects.com/en/2.2.x/errorhandling/


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMzIyMDc1NTQsLTEwNjAxNzYyNzIsMT
E5Njk2MjA2NCwtMTg2NjA3Mzg2OF19
-->