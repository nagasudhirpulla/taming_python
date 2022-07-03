## Skill - Forms in flask with WTForms 

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Serve static files in flask](https://nagasudhir.blogspot.com/2022/04/serve-static-files-in-flask.html)
* [Flask jinja templating](https://nagasudhir.blogspot.com/2022/04/jinja-templates-in-flask.html)
* [Macros in python flask jinja templates](https://nagasudhir.blogspot.com/2022/05/macros-in-python-flask-jinja-templates.html)
* [Forms with front-end and server-side validation in Flask web applications](https://nagasudhir.blogspot.com/2022/06/forms-with-front-end-and-server-side.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to create a form in a python flask web application and perform basic front-end and server-side form inputs validation

## Basic Form example with front-end validation
* The below `server.py` is a simple flask server
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
![flask_form_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/flask_form_demo.png)
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
* An additional "errors" object is passed into the template that contains the list of errors for each form input
* Notice that the form data is preserved after the post request also using the `request.form` variable in the jinja template 

```python
from flask import Flask, render_template, request

# create a server instance
app = Flask(__name__)

# configure a route handler
@app.route("/", methods=["GET", "POST"])
def index():
    errors = {}
    if request.method == "POST":
        uname = request.form["uName"]
        print("Name =", uname)
        print("Phone =", request.form["uPhone"])
        print("Email =", request.form["uEmail"])
                
        # check if the username starts with an alphabet
        if not uname[0].isalpha():
            errors["uName"] = ["username should start with alphabets"]
    return render_template("basic.html.j2", errors=errors)

# run the server
app.run(host="0.0.0.0", port=50100, debug=True)
```

```html
<!-- templates/home.html.j2 -->
<p>Hi, please fill this form</p>

<form method="post">
    <table>
        <tr>
            <td>Name</td>
            <td>
                <input type="text" name="uName" value="{{request.form['uName']}}" required minlength="4"/>
                <ul>
                {% for e in errors["uName"] %}
                    <li><span class="form-error">{{e}}</span></li>
                {% endfor %}
                </ul>
            </td>
        </tr>
        
        <tr>
            <td>Phone</td>
            <td>
                <input type="number" name="uPhone" value="{{request.form['uPhone']}}" required />
                <ul>
                {% for e in errors["uPhone"] %}
                    <li><span class="form-error">{{e}}</span></li>
                {% endfor %}
                </ul>
            </td>
        </tr>
        
        <tr>
            <td>Email</td>
            <td>
                <input type="email" name="uEmail" value="{{request.form['uEmail']}}" required />
                <ul>
                {% for e in errors["uEmail"] %}
                    <li><span class="form-error">{{e}}</span></li>
                {% endfor %}
                </ul>
            </td>
        </tr>

        <tr>
            <td><button type="submit">Submit</button></td>
        </tr>
    </table>
</form>

<style>
.form-error{
font-size: smaller;
color: red;
}
</style>
```

## Using macros to reduce repetitive HTML in jinja templates
* In the below example a macro named `render_input` is used to generate jinja template for each form input
* This reduces HTML repetition for rendering each form input thus reducing the scope for errors and increasing the readability of template 
```html
<!--templates/home.html.j2 file-->
<p>Hi, please fill this form</p>

{% macro render_input(label, inpName, inpType="text") %}
<tr>
    <td>{{label}}</td>
    <td>
        <input type="{{inpType}}" name="{{inpName}}" value="{{request.form[inpName]}}" {% for k,v in kwargs.items() %} {{k}}="{{v}}" {% endfor %} />
        <ul>
        {% for e in errors[inpName] %}
            <li><span class="form-error">{{e}}</span></li>
        {% endfor %}
        </ul>
    </td>
</tr>
{% endmacro %}

<form method="post">
    <table>
        {{render_input("Name", "uName", "text", minlength="4", required="")}}
        {{render_input("Phone", "uPhone", "number", required="")}}
        {{render_input("Email", "uEmail", "email", required="")}}
        <tr>
            <td><button type="submit">Submit</button></td>
        </tr>
    </table>
</form>

<style>
.form-error{
font-size: smaller;
color: red;
}
</style>
```

### Video
The video for this post can be seen [here](https://youtu.be/ve-3ho66a_E)

<iframe width="560" height="315" src="https://www.youtube.com/embed/ve-3ho66a_E" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## References
* Flask quickstart - https://flask.palletsprojects.com/en/2.1.x/quickstart/
* Jinja docs - https://jinja.palletsprojects.com/en/3.1.x/templates/
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4OTgyMDM1ODldfQ==
-->