## Skill - Flask jinja templating

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Serve static files in flask](https://nagasudhir.blogspot.com/2022/04/serve-static-files-in-flask.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

In this post we will learn how to use jinja templates for flask server side rendering

## if, elif, else in jinja template
```html
<!--index.html.j2 file-->
<html>
<body>
<h2>
{% if user.age <= 30 %}
{{ user.name }} is young
{% elif user.age >= 50 %}
{{ user.name }} is old
{% else %}
{{ user.name }} is not young
{% endif %}
</h2>
</body>
</html>
```
```py
# server python file
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html.j2', user={"name":"Abcd", "age": 52})

app.run(host='0.0.0.0', port=50100, debug=True)
```
### inline if else
```html
<!--index.html.j2 file-->
<html>
<body>
<h2>
{{ user.name }} is {{ 'old' if user.age>=50 else 'young' if user.age<=30 else 'not young' }}
</h2>
</body>
</html>
```

* inline if expression
* check if variable is defined in jinja2 - https://stackoverflow.com/questions/13956728/how-to-check-if-given-variable-exist-in-jinja2-template
* for loop in jinja2 templates
* getting for loop iterator in jinja2 using loop.index0
* create a range of numbers
* filters in jijna2
* decimal places display in jinja2 templates
* title case, upper case, lower case in jinja2
* macros in jinja2
* template inheritance
* jinja2 template docs - https://jinja.palletsprojects.com/en/3.1.x/templates/
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg1NjMyODYwNiwtMTk1MjA4NDI1LDE3OD
g2NjU0MjYsLTQ4NzIyOTUxNyw3MTU4ODc1NTMsMTgyNTU4MzI2
NCwtMjQzNzM0NDM1LC0xMDc0ODkxNDQ3LC0xODk1MTgxMzE4LD
EzMTY4NDQ1MzQsMTQ0MzcwMTcxOV19
-->