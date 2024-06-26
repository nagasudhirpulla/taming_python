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
* Additional keyword input arguments passed to the macros can be accessed using the special variable named `kwargs` inside the macro. 

## Calling jinja macro from another template file
* If the macro is declared in the same template file, it can be called directly.
* If the macro is present in another template file, it needs to be imported using the `{% from "<template_path>" import <macro_name> %}` jinja tags
* In the below template using jinja macro, repetitive jinja templating is reduced to render each form input

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

### Video
The video for this post can be seen [here](https://youtu.be/oq0V3o1DB7M)

<iframe width="560" height="315" src="https://www.youtube.com/embed/oq0V3o1DB7M" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* official docs - https://jinja.palletsprojects.com/en/3.1.x/templates/#macros
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg4ODc3NTI1LC0xMjA1MzUwMjIsLTE3Nz
U3MjUxMTEsNDcxMTIyMzU3LC01OTQ5MTI1MDBdfQ==
-->