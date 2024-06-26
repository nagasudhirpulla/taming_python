## Skill - WTForms for better forms validation and rendering in Flask 

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
* A jinja macro is used in the above example for rendering all the form fields to reduce jinja duplication 

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
* The form data of each field can be accessed using the data attribute. For example the data of the form field `form.uDob` can be accessed at `form.uDob.data`. The data will the desired form data type instead of string all the time. For example `form.uDob.data` will be a datetime object instead of string because WTForms will take the string from request.form and convert it to datetime object since the form field is declared as a `DateTimeField` field. Hence form data type interpretation is an additional benefit while using WTForms

### Additional form validation after form.validate()
* If extra validation is performed after `form.validate()` and errors are found, they can be populated in the `errors` attribute of the corresponding form field. For example, extra errors can be added to `form.uName` using `form.uName.errors.append("Username should start with an alphabet")`

### Video
The video for this post can be seen [here](https://youtu.be/j5IQI4aW9ZU)

<iframe width="560" height="315" src="https://www.youtube.com/embed/j5IQI4aW9ZU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## References
* WTForms - https://wtforms.readthedocs.io/en/3.0.x/fields/#basic-fields
* Flask quickstart - https://flask.palletsprojects.com/en/2.1.x/quickstart/
* Jinja docs - https://jinja.palletsprojects.com/en/3.1.x/templates/
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NDI2MzU2OTMsOTg0NDg5ODgxLC0xND
I3MDI1MDgsLTU5OTczMjQ0OCwxMDQ1Njg5NDE2LDE0NzY3NTA1
MzcsLTE5Mzk5NjM0MTIsLTk3MzE0MTYyNywtMTg1NjM2OTY3NS
wtMTkzNDQwOTAwNiwtMTczODUzOTIwOSwxMDQ3NDg1NjE0LDIx
MjE4NjQ2OTMsMTM4MjI0MjU4MywtMTY2MTEyNTQ5NiwtMTA2MD
gzMzkxNCwxNDMzMDcxNjQyLDUxNzM5NjE5OV19
-->