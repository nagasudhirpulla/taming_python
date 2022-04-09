
## Skill - Flask python module for building web servers

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* **flask** is a python library for creating web applications.
* It is easy and quick to learn flask

## Use cases
* Simple web interfaces for python applications can be build very quickly using flask
* flask can be used to create HTTP services or applications that require python modules like pandas, numpy etc

## Installing Flask
Install flask using pip with the following command
```
python -m pip install flask
```

## Simple Flask server
```python
from flask import Flask

# create a flask server
app = Flask(__name__)

# just return 'Hello World!' text when the route '/' is called
@app.route('/')
def index():
    return 'Hello, World!'

# __name__ will be __main__ only if this file is the entry point
if __name__ == '__main__':
    # run the server on this ip and port 50100
    app.run(host='0.0.0.0', port=50100, debug=True)
```
* In above example, the index function is assigned to server the route at '/' using the ```@app.route('/')``` decorator
* The content returned by the function will be returned to the client
* In this example, only plain text ```Hello, World!``` was returned. Instead HTML like ```<html><body><h2>Hello World!!!</h2></body></html>``` can also be returned so that the browser can interpret the HTML and display content.

## Multiple routes
```python
# just return 'Hello World!' text when the route '/' is called
@app.route('/')
def index():
    return 'Hello, World!'

# route for /hello
@app.route('/hello')
def hello():
    return '''<html>
                <body>
                    <h2>Hi there!!!</h2>
                    <a target="_blank" href="https://google.com">Google</a>
                </body>
            </html>'''
```

* In this example, two routes are handled by the server at '/' and '/hello' by two python functions

## Rendering response from a template
* The template files are to be stored in the 'templates' folder
```python
from flask import Flask, render_template

# create a flask server
app = Flask(__name__)

@app.route('/')
def index():
    return render_template('home.html.j2')

# __name__ will be __main__ only if this file is the entry point
if __name__ == '__main__':
    # run the server on this ip and port 50100
    app.run(host='0.0.0.0', port=50100, debug=True)
```
* ```home.html.j2``` can be a HTML file with jinja2 templating for server side rendering of data in the template file
```html
<html>
    <body>
        <h2>Hi there!!!</h2>
        <a target="_blank" href="https://google.com">Go to Google</a>
    </body>
</html>
```

## Rendering python variables in template file
* Python variables can be injected into the template as named parameters in the `render_template` function
* The data from python variables can be rendered in the template using jinja2 templating 
```python
from flask import Flask, render_template

# create a flask server
app = Flask(__name__)

@app.route('/')
def index():
    return render_template('home.html.j2', user={'name':'Abcd', 'city':'XYZ'})

# __name__ will be __main__ only if this file is the entry point
if __name__ == '__main__':
    # run the server on this ip and port 50100
    app.run(host='0.0.0.0', port=50100, debug=True)
```
* The `home.html.j2` file can be as shown below
```html
<html>
    <head><title>Jinja2 Template Example</title></head>
    <body>
        <h2>Hi {{ user.name }}!!!</h2>
        <h3>Your city is {{ user["city"] }}<h3>        
    </body>
</html>
```
## References
* Flask quickstart - https://flask.palletsprojects.com/en/2.1.x/quickstart/
* TODO check if variable is defined in jinja2 - https://stackoverflow.com/questions/13956728/how-to-check-if-given-variable-exist-in-jinja2-template
* TODO if condition in jinja2 templates
* TODO decimal places display in jinja2 templates
* TODO for loop in jinja2 templates
* jinja2 template docs - https://jinja.palletsprojects.com/en/3.1.x/templates/

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTEyMTY1MTM5NywxOTM3MDgyNTMyLDU1Nz
c0MjgzOSwxNjQyODM5MTAzLC0yMDkyODIxMTIwLDgwNDAwMDEw
Niw1ODUxNDMxNjksLTE2ODU2NDkyOTUsMTE0MDIzNTYwNiwyNT
YwNTMwNzUsMTU0NzY5NTE1OCw2NDY5OTgwMTZdfQ==
-->