## Skill - Serve static files in flask

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* Static files can be files like images, PDFs etc. that can be stored in the server folder and displayed or downloaded in the browser

## hosting static files
* Static files can be stored in a folder named "static" in the same folder as the server python file
* All static files can be accessible without any authorization, so do not host sensitive data in static folder
* URL for a static file can be generated dynamically without hard-coding using the `url_for` function. Example: url_for('static', 'img/abcd.png')
* `url_for` can be used directly in jinja template like `{{ url_for('static', 'img/abcd.png') }}`. For using `url_for` function in python code, we need to import it from flask module like `from flask import url_for`
### Example
* server.py file
```py
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def hi():
    return render_template("home.html.j2")

app.run(host='0.0.0.0', port=50100, debug=True)
```
* home.html.j2 template file
```html
<html>

<body>
    <a target="_blank" href="{{ url_for('static', filename='data/abcd.pdf') }}">Download the file</a>
    <br/>
    <img src="{{ url_for('static', filename='img/def.png') }}" alt="image file">
</body>

</html>
```
* ensure the following in the "static" folder
  * create a folder named 'data' and create a pdf file named 'abcd.pdf'
  * create a folder named 'img' and create a png file named 'def.png'

## change default static folder path and static folder URL
* Static files can be hosted in the folder named 'static' by default.
* To change the default static files folder, we can use the `static_folder` and `static_url_path` inputs while creating the flask application instance
* `static_folder` changes the folder from which the static files are served
* `static_url_path` changes the starting URL segment from which the static files are served
```py
# server python file
from flask import Flask, render_template

app = Flask(__name__, static_folder='reports', static_url_path='/reports')

@app.route('/')
def index():
    return render_template("home.html.j2")

app.run(host='0.0.0.0', port=50100, debug=True)
```

```html
<html>

<body>
    <a target="_blank" href="{{ url_for('static', filename='xyz.txt') }}">Download File</a>
</body>

</html>
```
* Even if we change any of the `static_folder` and `static_url_path`, we can still use 'static' as the first function argument while using `url_for` function

## host static files from additional folder using 'send_from_directory' function
* Suppose we desire to serve static files from a different folder (say 'reports') instead of 'static' folder
* We can use `send_from_directory` function to serve a file from desired folder, given the path of the file inside the folder
```py
# server python file
from flask import Flask, render_template, send_from_directory

app = Flask(__name__)

@app.route('/reports/<path:repPath>')
def send_report(repPath):
    return send_from_directory('reports', repPath)

@app.route('/')
def hi():
    return render_template("home.html.j2")

app.run(host='0.0.0.0', port=50100, debug=True)
```

```html
<!-- Template file -->
<html>

<body>
    <a target="_blank" href="{{ url_for('send_report', repPath='xyz.txt') }}">Download File</a>
</body>

</html>
```
* In the above python code, the 'send_report' function serves static files from the 'reports' folder. 
* The route used is `/reports/<path:repPath>`. Hence a variable named `repPath` can be passed from the URL to the send_report function. 
* Since we have mentioned the path segment as `<path:repPath>`, the route will be triggered only if the repPath segment is of type 'path'. If the path segment is of another type, the route will not be triggered.
* Authorization and authentication can also be imposed on this route that serves static files. This way we can also restrict the access of static files based on some authorization rules.

## serve single file from endpoint using 'send_file' function
* using the `send_file` function imported from flask, we can serve a single file
* In the below example, the 'report' function listening at the URL '/report' will serve the file 'xyz.pdf' using `send_file` function
```py
# server python file
from flask import Flask, render_template, send_file

app = Flask(__name__)

@app.route('/')
def index():
    return render_template("home.html.j2")

@app.route('/report')
def report():
    return send_file('./reports/xyz.pdf')

app.run(host='0.0.0.0', port=50100, debug=True)
```

```html
<!-- template file -->
<html>

<body>
    <a target="_blank" href="{{ url_for('report') }}">Download File</a>
</body>

</html>
```

### References
* serve files from a desired folder - https://stackoverflow.com/a/20648053/2746323
* https://stackoverflow.com/questions/43346486/change-static-folder-from-config-in-flask
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYyODI1ODE0OSwyMDYzNjQxNjE2LDE4ND
U4MjYzNjAsMTA1MTQ0NzQ1MiwyMDg3NTMwMjkwLDM0NjA5MjEz
NiwxNzU1NjI4NDU1LDE0NDk4MTY0MDksLTIwOTUzODI5NDMsMT
U3MTY0NTM5MCwxOTA2ODI4MjgsOTgzNzYxMzQ3XX0=
-->