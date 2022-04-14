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
```py
# server python file
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html.j2', user={"name":"Abcd", "age": 52})

app.run(host='0.0.0.0', port=50100, debug=True)
```

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
### check if variable is defined
* using the `is defined` operator we can get to know if the variable is defined in jinja template
```html
<!--index.html.j2 file-->
<html>
<body>
<h2>
{% if (user is defined) and (user.name is defined)%}
Hello {{ user.name }} !!!
{% else %}
username is not defined
{% endif %}
</h2>
</body>
</html>
```
### for loop in jinja templates
```html
<!-- template file -->
<html>
<body>
<h3>Users</h3>
<ul>
{% for u in users %}
<li>Name: {{ u.name }}, Age: {{ u.age }}</li>
{% endfor %}
</ul>
</body>
</html>
```
```py
# server python file
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html.j2', users=[
        {"name":"Abc", "age": 35},
        {"name":"Def", "age": 24},
        {"name":"Ghi", "age": 56},
        {"name":"Jkl", "age": 18}
    ])

app.run(host='0.0.0.0', port=50100, debug=True)
```
### getting for loop iterator in jinja using loop.index0 or loop.index
```html
<html>
<body>
<h3>Users</h3>
{% for u in users %}
<p>{{ loop.index }}. Name: {{ u.name }}, Age: {{ u.age }}</p>
{% endfor %}
</body>
</html>
```
* loop.index0 gives access to for 0-indexed (starts with 0) for loop iterator
* loop.index gives access to  1-indexed (starts with 1) for loop iterator
* Other properties of loop variable inside a for loop can be found at https://jinja.palletsprojects.com/en/3.0.x/templates/#for

### create a sequence of numbers in jinja using 'range' function
```html
<!--template file-->
<html>
<body>
<h3>jinja range example for generating sequence of numbers just like python</h3>
{% for x in range(6) %}
<p>{{ x }}</p>
{% endfor %}
</body>
</html>
```
### filters in jinja templates
* filters in jinja are like functions in python. 
* If we use a function like `upper(x)` in python, we use `{{ x|upper }}` in jinja using the `|` operator
* In python if we pass parameters like `round(x, 2)`, we use `{{ x|round(2) }}` to pass additional parameters

#### count filter
```html
<!--template file-->
<html>
<body>
<h3>count of items</h3>
<span>Number of users = {{ users|count }}</span>
</body>
</html>
```
#### join filter
```html
<!--template file-->
<html>
<body>
<h3>count of items</h3>
<span>Number of users = {{ users|count }}</span>
</body>
</html>
```

#### round and int filters
```html
<!--template file-->
<html>
<body>
<h3>Using round and int filters for decimals manipulation of numbers</h3>
<p>{{ 45.2|int }}</p>
<p>{{ 45.247|round(2) }}</p>
<p>{{ 45.247|round(2, 'floor') }}</p>
</body>
</html>
```
#### escape filter
```html
<!--template file-->
<html>
<body>
<h3>escape filter for html escaping while rendering</h3>
<span>{{'<script>var x = "injection risk"</script>'|escape}}</span>
</body>
</html>
```

* title case, upper case, lower case, trim in jinja2
* join filter
* escape filter for HTML escaping


### References
* jinja2 docs - https://jinja.palletsprojects.com/en/3.1.x/templates/
* check if variable is defined in jinja2 - https://stackoverflow.com/questions/13956728/how-to-check-if-given-variable-exist-in-jinja2-template
* for loop in jinja - https://jinja.palletsprojects.com/en/3.1.x/templates/#jinja-globals.range
*  built in filters in jinja2 - https://jinja.palletsprojects.com/en/3.1.x/templates/#list-of-builtin-filters
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ3NDYyNzg3LC0xODI5ODk2ODIzLC05Mz
k5OTE5OTIsLTMwOTI4NTMxOCwtMTcxNTI2NTQyNiwtNDUyNTE2
NDA0LC00MTUwMTg5MjUsLTE2MDU1ODczMjAsMTI3MzgwOTE5OS
wxMjM0Mjc2OTA0LC00Mjc5NTMwNzIsMTk3ODg2NTI0OSwxMjYw
MTM1ODUxLC0xOTUyMDg0MjUsMTc4ODY2NTQyNiwtNDg3MjI5NT
E3LDcxNTg4NzU1MywxODI1NTgzMjY0LC0yNDM3MzQ0MzUsLTEw
NzQ4OTE0NDddfQ==
-->