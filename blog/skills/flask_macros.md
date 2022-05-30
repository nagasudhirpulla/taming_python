## Skill - Macros in python flask jinja templates

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Serve static files in flask](https://nagasudhir.blogspot.com/2022/04/serve-static-files-in-flask.html)
* [Flask jinja templating](https://nagasudhir.blogspot.com/2022/04/jinja-templates-in-flask.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to reduce repetition in flask templates using macros in flask jinja templates  
* Jinja macro will render a jinja template based on the inputs provided to it. Jinja macro is similar to a function in python

## Example
* The below server.py is a simple flask server
* It serves `home.html.j2` template present in the `templates` folder
* The page can be accessed at `http://localhost:50100`
```py
# server.py file
from flask import Flask, render_template

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("home.html.j2")

app.run(host="0.0.0.0", port=50100, debug=True)
```

## Example Jinja macro
```html
<!-- templates/_formhelpers.html.j2 file -->
{% macro render_input(label, inpName, inpType="text", showErrors="true", errors=[]) %}
<tr>
    <td>{{label}}
    </td>
    <td>
        <input type="{{inpType}}" name="{{inpName}}" {% for k,v in kwargs.items() %} {{k}}="{{v}}" {% endfor %} />
        <ul class="errors">
        {% for err in errors %}
            <li>{{ err }}</li>
        {% endfor %}
        </ul>
    </td>
</tr>
{% endmacro %}
```
* In the above example, a macro named `render_input` is declared using the `{% macro %} {% endmacro %}` jinja tags
* The inputs of macro are declared just like python functions. Default input values can also be declared
* All the jinja template in between the `{% macro %} {% endmacro %}` tags will be rendered based on the input parameters when the macro is called

## Calling jinja macro from another template file
* If the macro is declared in the same template file, it can be called directly.
* If the macro is present in another template file, it needs to be imported using the `{% from "<template>" import  %}`
```html
<!--templates/home.html.j2 file-->
{% from "_formhelpers.html.j2" import render_input %}
<form>
<table>
{{render_input(label="name", inpName="username")}}
{{render_input(label="phone", inpName="userPhone", inpType="number", class="phone")}}
{{render_input(label="email", inpName="userEmail", inpType="email", size=100, class="email")}}
</table>
</form>
```

### Child Template
* Child templates can extend the base template using the 'extends' tag. For example, in the `home.html.j2` , `{% extends "base/layoutBase.html.j2" %}` is used to indicate that the template extends the base template at `base/layoutBase.html.j2`
* Child templates can fill the base template blocks with content. For example, in the child template `home.html.j2` using `{% block content %}{% endblock %}` , the child template is filling the block named "content" with its own HTML or jinja content.
* While overwriting the parent block contents, Child templates can retain the base template block content and add extra HTML before or after it using `{{ super ()}}` . If the base block is not overwritten, the base block content will be rendered in the child template. 
	* For example, inside the `head` block of the `home.html.j2` file, an additional script tag is added below `{{ super() }}`. Hence the base template block content will be rendered first and then the script tag will be rendered.

```html
<!--templates/home.html.j2 file-->
{% extends "base/layoutBase.html.j2" %}
{% block title %}Home{% endblock %}

{% block head %}
{{ super() }}
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.29.2/moment.min.js"></script>
{% endblock %}

{% block content %}
<h2>Hello World!!!</h2>
{% endblock %}

{% block scripts %}
<style>
html,
body {
  height: 100%;
}
</style>
{% endblock %}  
```

### static files required for this example
* For this example to work, JavaScript and CSS libraries are required to be hosted in the `static/node_modules` folder.
* We can use npm to generate the required files.
* Create a file named `package.json` in the 'static' folder and paste the following in it.
```json
{
    "name": "sample_app",
    "version": "1.0.0",
    "description": "",
    "dependencies": {
        "@fortawesome/fontawesome-free": "^5.14.0",
        "bootstrap": "^4.5.2",
        "jquery": "^3.5.1",
        "startbootstrap-sb-admin-2": "^4.1.1"
    }
}
```
* Open a command inside the 'static' folder and run the command `npm install`. Then all the required libraries will be downloaded into the `static/node_modules` folder. Using npm requires Node JS installed with an internet connection

### Video
The video for this post can be seen [here](https://youtu.be/OCk_ahHML4I)

<iframe width="560" height="315" src="https://www.youtube.com/embed/OCk_ahHML4I" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* official docs - https://jinja.palletsprojects.com/en/3.1.x/templates/#template-inheritance
* 'include' tag in jinja - https://jinja.palletsprojects.com/en/3.1.x/templates/#include
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNzg4MjE1NzUsNDcxMTIyMzU3LC01OT
Q5MTI1MDBdfQ==
-->