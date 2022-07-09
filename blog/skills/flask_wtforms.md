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

* In this post we will learn how to use WTForms for efficient and easy forms management in Flask web applications.
* WTForms also helps in writing less code and reducing the scope of manual errors while creating forms in flask

## Installing WTForms
* WTForms can be installed in a python environment with pip using the following command
```bat
python -m pip install WTForms
``` 

## The Use Case
* To explain the usage of WTForms in this blog post, we are considering an example of a user registration form as shown below
![wtforms_example_form image](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/wtforms_example_form.PNG)

## The Form object
* The labels, data types, names etc of all the form fields can be defined as an object of the `Form` class from the wtforms library
* This form object can be used to easily accomplish the following tasks 
	* render form inputs in the template
	* perform server-side form inputs validation
	* extract form data
	* create error messages for invalid form inputs
* As shown below a class named `UserRegisterForm` inherited from `Form` class can be created for our example

```py
from wtforms import Form, validators, StringField, BooleanField, DateTimeField, SelectField, PasswordField
from wtforms.fields import html5 as h5fields
from wtforms.widgets import html5 as h5widgets
from wtforms.widgets import TextArea

class UserRegisterForm(Form):
    uName = StringField("Name", validators=[
                        validators.InputRequired(), validators.Length(min=4, max=250)])
    uPass = PasswordField("Password", validators=[
                        validators.InputRequired(), validators.Length(min=4, max=15)])
    uPhone = h5fields.IntegerField("Phone", validators=[validators.InputRequired(
    )], widget=h5widgets.NumberInput(min=6000000000, step=1, max=9999999999))
    uEmail = StringField("Email", validators=[validators.InputRequired()])
    isGetEmails = BooleanField("Get Promotional Emails", default=False)
    uDob = DateTimeField("Date of Birth", validators=[
                         validators.Optional()], format='%Y-%m-%d')
    uGender = SelectField("Gender", validators=[validators.InputRequired()], choices=[
                          (0, "Male"), (1, "Female"), (2, "Other")])
    uAboutMe = StringField("About Yourself", validators=[
                           validators.Optional(), validators.length(max=300)], widget=TextArea())
```

* The fields defined in the above Form object are `StringField`, `PasswordField`, `IntegerField`, `BooleanField`, `DateTimeField`, `SelectField`
* validators and other options can be defined in the field initialization
* The first input to the Field class initialization would be the label of the field
* While defining the `SelectField`, an input named `choices` can be provided as a list of tuples of (value, text). These tuples will define the options of the select list
* For `DateTimeField`, the `format` input will specify the time string format in which the input should be provided in the web page
* For defining a `textarea` input, additional input of `widget=TextArea()` can be provided to the `StringField`

## Injecting form object into the template
* The below `server.py` is a simple flask server accessible at `http://localhost:50100` which serves `home.html.j2` template present in the `templates` folder
* The form object named `form` is initialized and injected into the template as shown below in the line `return render_template("home.html.j2", form=form)`

```py
# server.py file
from flask import Flask, render_template, request
# create a server instance
app = Flask(__name__)

# route handler
@app.route("/", methods=["GET", "POST"])
def index():
    form = UserRegisterForm(request.form)
    return render_template("home.html.j2", form=form)

# run the server
app.run(host="0.0.0.0", port=50100, debug=True)
```

### Rendering each form field
```html
<p>Hi, please fill this form</p>

{% macro render_input(field, showErrors="true") %}
    <tr>
        <td>{{ field.label }}</td>
        <td>{{ field(**kwargs)|safe }}
            {% if showErrors=="true" and field.errors %}
            <ul class="errors">
            {% for error in field.errors %}
                <li>{{ error }}</li>
            {% endfor %}
            </ul>
            {% endif %}
        </td>
    </tr>
{% endmacro %}

<form method="post">
    <table>
        {{render_input(form.uName)}}
        {{render_input(form.uPass)}}
        {{render_input(form.uPhone)}}
        {{render_input(form.uEmail, type="email")}}
        {{render_input(form.isGetEmails)}}
        {{render_input(form.uDob, type="date")}}
        {{render_input(form.uGender)}}
        {{render_input(form.uAboutMe)}}
        <tr>
            <td><button type="submit">Submit</button></td>
        </tr>
    </table>
</form>

<style>
.errors{
    font-size: 0.5em;
    color: red;
}
</style>
```

* A form field say `form.uName` can be rendered in the template using `{{ form.uName()|safe }}`
* Extra HTML attributes of the input field can be rendered by just passing them as named attributes like `{{ form.uEmail(type="date") }}`
* The label of the input field can be accessed using the ".label" attribute of the input field like `{{ form.uDob.label }}`
* The errors in each form field derived from the server-side will be stored in the ".errors" attribute. For example the errors of the form field `form.uPhone` will be stored in `form.uPhone.errors` as a list of strings which can be rendered in the template for displaying to the user after server-side form validation

### Front-end validation
* If the validators of the form fields in the form object are straightforward like `validators.Required`, the required HTML tags for front end validation are rendered in the `{{form.field()|safe}}` itself. This is an additional advantage of using WTForms
* If additional attributes for front-end valdation are required, those can be explicitly mentioned during rendering, for example `{{ form.uEmail(type="date") }}`
* Third-party JavaScript libraries like validator.js can also be used for front-end validation in the browser

### Server-side Form handling
* Below is the flask server code to handle the form submission in our example

```py
from flask import Flask, render_template, request
from wtforms import Form, validators, StringField, BooleanField, DateTimeField, SelectField, PasswordField
from wtforms.fields import html5 as h5fields
from wtforms.widgets import html5 as h5widgets
from wtforms.widgets import TextArea

# create a server instance
app = Flask(__name__)

# create form object
class UserRegisterForm(Form):
    uName = StringField("Name", validators=[
                        validators.InputRequired(), validators.Length(min=4, max=250)])
    uPass = PasswordField("Password", validators=[
                        validators.InputRequired(), validators.Length(min=4, max=15)])
    uPhone = h5fields.IntegerField("Phone", validators=[validators.InputRequired(
    )], widget=h5widgets.NumberInput(min=6000000000, step=1, max=9999999999))
    uEmail = StringField("Email", validators=[validators.InputRequired()])
    isGetEmails = BooleanField("Get Promotional Emails", default=False)
    uDob = DateTimeField("Date of Birth", validators=[
                         validators.Optional()], format='%Y-%m-%d')
    uGender = SelectField("Gender", validators=[validators.InputRequired()], choices=[
                          (0, "Male"), (1, "Female"), (2, "Other")])
    uAboutMe = StringField("About Yourself", validators=[
                           validators.Optional(), validators.length(max=300)], widget=TextArea())

# route handler
@app.route("/", methods=["GET", "POST"])
def index():
    form = UserRegisterForm(request.form)
    if request.method == "POST" and form.validate():
        uName = request.form["uName"]
        print("User =", uName)
        print("Password =", form.uPass.data)
        print("Phone =", form.uPhone.data)
        print("Email =", form.uEmail.data)
        print("Get Emails =", form.isGetEmails.data)
        print("Date of Birth =", form.uDob.data)
        print("Gender =", form.uGender.data)
        print("About Me =", form.uAboutMe.data)
        if not uName[0].isalpha():
            form.uName.errors.append("Username should start with an alphabet")
    return render_template("home.html.j2", form=form)

# run the server
app.run(host="0.0.0.0", port=50100, debug=True)
```

* The form object along with the user inputs can be retrieved using the `request.form` object. For example in our case we created a form object using `form = UserRegisterForm(request.form)`
* To handle the POST request sent by the browser, an additional parameter `methods=["GET", "POST"]` is specified in the route handler decorator. This means that the route handler will also accept "POST" requests also in addition to "GET" requests. Using `request.method` inside the route handler, we can differentiate whether the route handler is triggered by a "GET" or "POST" request.
* The form object can be validated just by calling `form.validate()` which returns True if the form inputs are passing the `validators` of all form fields. Thus validation is very easy and less error prone when we use WTForms
* After calling `form.validate()`, any errors in each form field are populated in the errors attribute as a list of strings. For example the errors of the `form.uEmail` field can be accessed at `form.uEmail.errors`. All the errors of the form can also be accessed using `form.errors` 

### Additional form validation after form.validate()
* If extra validation is performed after `form.validate()` and errors are found, they can be populated in the `errors` attribute of the corresponding form field. For example, extra errors can be added to `form.uName` using `form.uName.errors.append("Username should start with an alphabet")`

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
* WTForms - https://wtforms.readthedocs.io/en/3.0.x/fields/#basic-fields
* Flask quickstart - https://flask.palletsprojects.com/en/2.1.x/quickstart/
* Jinja docs - https://jinja.palletsprojects.com/en/3.1.x/templates/
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk3NTEyOTIwNSwtMTQyNzAyNTA4LC01OT
k3MzI0NDgsMTA0NTY4OTQxNiwxNDc2NzUwNTM3LC0xOTM5OTYz
NDEyLC05NzMxNDE2MjcsLTE4NTYzNjk2NzUsLTE5MzQ0MDkwMD
YsLTE3Mzg1MzkyMDksMTA0NzQ4NTYxNCwyMTIxODY0NjkzLDEz
ODIyNDI1ODMsLTE2NjExMjU0OTYsLTEwNjA4MzM5MTQsMTQzMz
A3MTY0Miw1MTczOTYxOTldfQ==
-->