## Skill - Flask jinja templating

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Serve static files in flask](https://nagasudhir.blogspot.com/2022/04/serve-static-files-in-flask.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

In this post we will learn how to use jinja templates for flask server side rendering
<br/>
The topics covered are
* if, elif, else in jinja template
* inline if else
* check if variable is defined
* for loop in jinja templates
* 

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
<h3>join filter to combine items</h3>
<p>{{ range(10)|join(", ") }}</p>
<p>{{ users|join(", ", attribute='name') }}</p>
</body>
</html>
```
* Using the `attribute` input to the join filter, we can also specify the attribute of the object we want to join.
* In the above example, only `name` attribute of each user object is used for joining\

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

#### upper, lower, title, capitalize, trim filters
```html
<!--template file-->
<html>
<body>
<p>upper 'hi, how are you...' , all characters are upper cased</p>
<p>{{'hi, how are you...'|upper}}</p>
<br/>

<p>lower 'Hi, HOW are yOu...' , all characters are lower cased</p>
<p>{{'Hi, HOW are yOu...'|lower}}</p>
<br/>

<p>title 'Hi, HOW are yOu...' , starting character of each word is capitalized</p>
<p>{{'Hi, HOW are yOu...'|title}}</p>
<br/>

<p>trim '   Hi, HOW are yOu... ' , starting and ending spaces are trimmed</p>
<p>{{'Hi, HOW are yOu...'|trim}}</p>
<br/>

<p>capitalize 'hi, HOW are yOu...' , Only first character is capitalized</p>
<p>{{'hi, HOW are yOu...'|capitalize}}</p>
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

### References
* jinja2 docs - https://jinja.palletsprojects.com/en/3.1.x/templates/
* check if variable is defined in jinja2 - https://stackoverflow.com/questions/13956728/how-to-check-if-given-variable-exist-in-jinja2-template
* for loop in jinja - https://jinja.palletsprojects.com/en/3.1.x/templates/#for
*  built in filters in jinja2 - https://jinja.palletsprojects.com/en/3.1.x/templates/#list-of-builtin-filters
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM3ODEwMDUyOCwxNDM3NjY1OTQ2LDE2Nj
M3NzQ2NTYsLTQ3NDYyNzg3LC0xODI5ODk2ODIzLC05Mzk5OTE5
OTIsLTMwOTI4NTMxOCwtMTcxNTI2NTQyNiwtNDUyNTE2NDA0LC
00MTUwMTg5MjUsLTE2MDU1ODczMjAsMTI3MzgwOTE5OSwxMjM0
Mjc2OTA0LC00Mjc5NTMwNzIsMTk3ODg2NTI0OSwxMjYwMTM1OD
UxLC0xOTUyMDg0MjUsMTc4ODY2NTQyNiwtNDg3MjI5NTE3LDcx
NTg4NzU1M119
-->