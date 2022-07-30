## Skill - Directory Listing in Flask

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Serve static files in flask](https://nagasudhir.blogspot.com/2022/04/serve-static-files-in-flask.html)
* [Flask jinja templating](https://nagasudhir.blogspot.com/2022/04/jinja-templates-in-flask.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how show a list of files present in the server directory along with navigation and download features using Flask 
 

## Use Cases
* Directory listing may be useful if we desire to display files of a particular folder in a server like generated reports, images etc. 

## Basic server
* The following python server acts as a flask server that runs on port 50100
* We will add the directory listing to this server
```py
from flask import Flask

# create a server instance
app = Flask(__name__)

@app.route('/')
def index():
    return "Hello World!!!"

# run the server
app.run(host="0.0.0.0", port=50100, debug=True)
```

## Get all the folder contents using os.scandir
* For a given folder path, all the files and folder inside the folder can be fetched using the `os.scandir` function
```py
import os
folderPath = r"C:\"
print([x.name for x in os.scandir(folderPath)])
```

## Get the file size and modified time with os.stat
* The file size and last modified time for a file path can be derived from `os.stat` function
```py
import os

filePath = r'C:\Windows\regedit.exe'
fileStat = os.stat(filePath)

print(f"fileSize = {fileStat.st_size} bytes")
print(f"Modified Time in posix timestamp = {fileStat.st_mtime}")
```
* We can use helper functions to make the file size (in bytes) and modified time (POSIX timestamp) more readable as shown in the below example

```py
import os
import datetime as dt

def getReadableByteSize(num, suffix='B') -> str:
    for unit in ['', 'Ki', 'Mi', 'Gi', 'Ti', 'Pi', 'Ei', 'Zi']:
        if abs(num) < 1024.0:
            return "%3.1f%s%s" % (num, unit, suffix)
        num /= 1024.0
    return "%.1f%s%s" % (num, 'Yi', suffix)


def getTimeStampString(tSec: float) -> str:
    tObj = dt.datetime.fromtimestamp(tSec)
    tStr = dt.datetime.strftime(tObj, '%Y-%m-%d %H:%M:%S')
    return tStr

filePath = r'C:\Windows\regedit.exe'
fileStat = os.stat(filePath)

print(f"fileSize = {getReadableByteSize(fileStat.st_size)} bytes")
print(f"Modified Time in posix timestamp = {getTimeStampString(fileStat.st_mtime)}")
```

## Deriving file path from URL using safe_join 
* The path of the file is expressed as a URL path in directory listing
* Path of the desired file in the file system can be derived using this URL path just by joining the base folder path with the URL path 
* For example, if the request URL was `/Web/Screen/img102.jpg` and the base folder is located at  `C:\Abcd`, the desired file path would be `C:\Abcd\Web\Screen\img102.jpg`
* This can be achieved using `safe_join` function from flask as shown below
```py
from flask import safe_join
urlPath = 'Web/Screen/img102.jpg'
baseFolderPath = r'C:\Abcd'
print('filePath=',safe_join(baseFolderPath, urlPath).replace('\\', '/'))
```
* The advantage of using `safe_join` over `os.path.join` is that it ensures that files above the server base folder are not served. Hence a security issue can be addressed using safe_join function

## Get parent folder path of a folder using pathlib
* For navigational purposes, we need to create a link for the parent folder of the current folder being displayed
* This can be 


## Injecting form object into the template
* The below `server.py` is a simple flask server accessible at `http://localhost:50100` which serves `home.html.j2` template present in the `templates` folder
* The form object named `form` is initialized and injected into the template as shown below in the line `return render_template("home.html.j2", form=form)`

```py
from flask import Flask, render_template, abort, safe_join, send_file
from pathlib import Path
import os
import datetime as dt

# create a server instance
app = Flask(__name__)
FolderPath = r"C:\Users\Nagasudhir\Downloads"

@app.route('/')
def index():
    return "Hello World!!!"

def getReadableByteSize(num, suffix='B') -> str:
    for unit in ['', 'Ki', 'Mi', 'Gi', 'Ti', 'Pi', 'Ei', 'Zi']:
        if abs(num) < 1024.0:
            return "%3.1f%s%s" % (num, unit, suffix)
        num /= 1024.0
    return "%.1f%s%s" % (num, 'Yi', suffix)

def getTimeStampString(tSec: float) -> str:
    tObj = dt.datetime.fromtimestamp(tSec)
    tStr = dt.datetime.strftime(tObj, '%Y-%m-%d %H:%M:%S')
    return tStr

def getIconClassForFilename(fName):
    fileExt = Path(fName).suffix
    fileExt = fileExt[1:] if fileExt.startswith(".") else fileExt
    fileTypes = ["aac", "ai", "bmp", "cs", "css", "csv", "doc", "docx", "exe", "gif", "heic", "html", "java", "jpg", "js", "json", "jsx", "key", "m4p", "md", "mdx", "mov", "mp3",
                 "mp4", "otf", "pdf", "php", "png", "pptx", "psd", "py", "raw", "rb", "sass", "scss", "sh", "sql", "svg", "tiff", "tsx", "ttf", "txt", "wav", "woff", "xlsx", "xml", "yml"]
    fileIconClass = f"bi bi-filetype-{fileExt}" if fileExt in fileTypes else "bi bi-file-earmark"
    return fileIconClass

# route handler
@app.route('/getFiles/', defaults={'reqPath': ''})
@app.route('/getFiles/<path:reqPath>')
def getFiles(reqPath):
    # Join the base and the requested path
    # could have done os.path.join, but safe_join ensures that files are not fetched from parent folders of the base folder
    absPath = safe_join(FolderPath, reqPath)

    # Return 404 if path doesn't exist
    if not os.path.exists(absPath):
        return abort(404)

    # Check if path is a file and serve
    if os.path.isfile(absPath):
        return send_file(absPath)

    # Show directory contents
    def fObjFromScan(x):
        fileStat = x.stat()
        # return file information for rendering
        return {'name': x.name,
                'fIcon': "bi bi-folder-fill" if os.path.isdir(x.path) else getIconClassForFilename(x.name),
                'relPath': os.path.relpath(x.path, FolderPath).replace("\\", "/"),
                'mTime': getTimeStampString(fileStat.st_mtime),
                'size': getReadableByteSize(fileStat.st_size)}
    fileObjs = [fObjFromScan(x) for x in os.scandir(absPath)]
    # get parent directory url
    parentFolderPath = os.path.relpath(
        Path(absPath).parents[0], FolderPath).replace("\\", "/")
    return render_template('home.html.j2', data={'files': fileObjs,
                                                 'parentFolder': parentFolderPath})

# run the server
app.run(host="0.0.0.0", port=50100, debug=True)
```

### Template file
```html
<h2>Directory Listing Example</h2>
<table class="table table-striped table-responsive">
    <thead>
        <tr>
            <th>Name</th>
            <th>Modified Time</th>
            <th>Size</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <a href="{{ url_for('getFiles', reqPath=data['parentFolder']) }}">
                    <span><i class="bi bi-folder-symlink" style="margin-right:0.3em"></i>Parent Directory</span>
                </a>
            </td>
            <td></td>
            <td></td>
        </tr>
        {% for fileObj in data['files'] %}
        <tr>
            <td>
                <a href="{{ url_for('getFiles', reqPath=fileObj['relPath']) }}">
                    <span><i class="{{fileObj['fIcon']}}" style="margin-right:0.3em"></i>{{ fileObj['name'] }}</span>
                </a>
            </td>
            <td>{{fileObj['mTime']}}</td>
            <td>{{fileObj['size']}}</td>
        </tr>
        {% endfor %}
    </tbody>
</table>

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.9.1/font/bootstrap-icons.css">

<style>
table {table-layout:fixed; width:100%;}
table td, th {word-wrap:break-word;}
th {text-align: left;}
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
eyJoaXN0b3J5IjpbMTM0ODYyNDE1OCwxNjU0MDg1MjQwLDE0OT
A0NDcyNjgsLTE1NDY5Mjg1MTUsLTE4MzYwNDQ1MDMsLTE5MzE2
MTMwODgsLTEyNTc0MTY4NDldfQ==
-->