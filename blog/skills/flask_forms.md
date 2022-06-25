## Skill - Forms with basic front-end and server-side validation in Flask web application

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Serve static files in flask](https://nagasudhir.blogspot.com/2022/04/serve-static-files-in-flask.html)
* [Flask jinja templating](https://nagasudhir.blogspot.com/2022/04/jinja-templates-in-flask.html)
* [Macros in python flask jinja templates](https://nagasudhir.blogspot.com/2022/05/macros-in-python-flask-jinja-templates.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to create a form in a python flask web application and perform basic front-end and server-side form inputs validation

## Basic Form example with front-end validation
* The below server.py is a simple flask server
* It serves `home.html.j2` template present in the `templates` folder
* The page can be accessed at `http://localhost:50100`
* The page contains a simple form with 3 inputs for capturing name, phone and email
```py
# server.py file
from flask import Flask, render_template, request

# create a server instance
app = Flask(__name__)

# configure a route handler
@app.route("/", methods=["GET", "POST"])
def index():
    if request.method == "POST":
        print("Name =", request.form["uName"])
        print("Phone =", request.form["uPhone"])
        print("Email =", request.form["uEmail"])
    return render_template("basic.html.j2")

# run the server
app.run(host="0.0.0.0", port=50100, debug=True)
```

```html
<!-- templates/home.html.j2 file -->
<p>Hi, please fill this form</p>

<form method="post">
    <table>
        <tr>
            <td>Name</td>
            <td>
                <input type="text" name="uName" required minlength="4" />
            </td>
        </tr>
        
        <tr>
            <td>Phone</td>
            <td>
                <input type="number" name="uPhone" required />
            </td>
        </tr>
        
        <tr>
            <td>Email</td>
            <td>
                <input type="email" name="uEmail" required />
            </td>
        </tr>

        <tr>
            <td><button type="submit">Submit</button></td>
        </tr>
    </table>
</form>
```

### Anatomy of a basic Form 
* A form is created in the above jinja template using the `form` tag
* Each form input is given a `name` attribute to identify the various inputs at the server side after the form is submitted
* A button with the `type` attribute as "submit" is created inside the form tag to facilitate a form submit button.
* Once the user clicks the submit button, a "POST" request is sent to the same page where the form inputs can be processed by the server's route handler

### Front-end validation
* Front-end input validation in the browser can be achieved using simple HTML attributes like "required", "minlength", "min", "max"
* Third-party JavaScript libraries like validator.js can also be used for front-end validation in the browser

### Server-side Form handling
* To handle the POST request sent by the browser, an additional parameter `methods=["GET", "POST"]` is specified in the route handler decorator. This means that the route handler will also accept "POST" requests also in addition to "GET" requests
* Using `request.method` inside the route handler, we can differentiate whether the route handler is triggered by a "GET" or "POST" request.

### Accessing Form data in route handler
* The `request.form` object inside the route handler will contain the form data as a dictionary
* For example in the "POST" request route handler, `request.form["uName"]` will have the username entered in the form since "uName" is the "name" attribute of the username HTML input tag

## Server-side Form inputs validation
* Performing server side form validation is important since the browser is not in the server's control and complex inputs validations may not be implemented in the browser
* Hence server-side form validation is important for improving the forms security and complex validation scenarios

### Server side form validation example
* In the following server code, the user name of the form is validated in the route handler to check if user name starts with an alphabet.
* An additional "errors" object s 

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
eyJoaXN0b3J5IjpbLTE0NzQ4MjQ1LDExOTE1MTIxNTQsMjk4NT
EzODM4LDE2NzU2NjEzNTgsLTc2OTE2ODE3NSwtMjA3NTQ3NTM2
MSwxOTI2ODEwNTk0LDIwMTU1NzMxMDYsNTExNDg2OTIyLC0xOD
I4MTg5MzI0LC0xNTIxMDQwNTk2XX0=
-->