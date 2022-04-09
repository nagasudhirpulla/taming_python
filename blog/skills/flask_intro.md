## Skill - Flask python module introduction for creating web servers

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
* Simple web interfaces for python applications can be build very easily with flask
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
* In above example, the index function is assigned to serve the route at '/' using the ```@app.route('/')``` decorator
* The content returned by the function will be returned to the client or browser
* In this example, only plain text ```Hello, World!``` was returned. Instead HTML like ```<html><body><h2>Hello World!!!</h2></body></html>``` can also be returned so that the browser can interpret the HTML and display content.

## Multiple routes
```python
# route for '/'
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
    return render_template('home.html.j2', user={'name':'Abcd', 'city':'XYZ'}, numViews=1234)

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
        <span>number of views = {{ numViews }}</span>        
    </body>
</html>
```
## References
* Flask quickstart - https://flask.palletsprojects.com/en/2.1.x/quickstart/


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkyMjY2MjU4Miw3NTc1ODcxNTMsNzYwNT
UzOTM2LC0xMTAyNTI3OTYzLDE5MzcwODI1MzIsNTU3NzQyODM5
LDE2NDI4MzkxMDMsLTIwOTI4MjExMjAsODA0MDAwMTA2LDU4NT
E0MzE2OSwtMTY4NTY0OTI5NSwxMTQwMjM1NjA2LDI1NjA1MzA3
NSwxNTQ3Njk1MTU4LDY0Njk5ODAxNl19
-->