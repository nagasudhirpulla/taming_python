## Skill - Template inheritance in Flask jinja

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Serve static files in flask](https://nagasudhir.blogspot.com/2022/04/serve-static-files-in-flask.html)
* [Flask jinja templating](https://nagasudhir.blogspot.com/2022/04/jinja-templates-in-flask.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to use Template Inheritance in flask jinja templates for creating reusable and complex web layouts
* We can build a **base template** that can be extended by **child templates**. This enables *re-usability*, *template splitting* and *consistency* in the layout of all the web application pages

## Demo Layout
* In this post we will create a reusable base layout for flask applications using Base Templates concept
* The base layout is based on the SB Admin 2 theme at https://startbootstrap.com/theme/sb-admin-2
* The server.py file is a simple flask server a shown below
```py
# server.py file
from flask import Flask, render_template

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("home.html.j2")

app.run(host="0.0.0.0", port=50100, debug=True)
```
![sb_admin_template](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/sb_admin_template.png)
## Base Template
* It is just just a jinja template with named blocks in it.
* Child templates can fill the blocks with content. For example, in the base template using `{% block content %}{% endblock %}` , the child template can fill the block named "content" with its own HTML or jinja content.
```html
<!--templates/base/layoutBase.html.j2 file-->
<!DOCTYPE html>
<html lang="en">

<head>
    {% block head %}
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>{% block title %}{% endblock %} - Sample App</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='node_modules/bootstrap/dist/css/bootstrap.min.css') }}" />

    <!-- Custom fonts for sb admin 2-->
    <link href="{{ url_for('static', filename='node_modules/@fortawesome/fontawesome-free/css/all.min.css') }}" rel="stylesheet" type="text/css">
    <link href="https://fonts.googleapis.com/css?family=Nunito:200,200i,300,300i,400,400i,600,600i,700,700i,800,800i,900,900i" rel="stylesheet">

    <!-- Custom styles for sb-admin-2-->
    <link href="{{ url_for('static', filename='node_modules/startbootstrap-sb-admin-2/css/sb-admin-2.min.css') }}" rel="stylesheet"> {% endblock %}
</head>

<body id="page-top">
    <div id="wrapper">
        <!--Sidebar-->
        <ul class="navbar-nav bg-gradient-primary sidebar sidebar-dark accordion" id="accordionSidebar">
            <!-- Sidebar - Brand -->
            <a class="sidebar-brand d-flex align-items-center justify-content-center" href="{{ url_for('index') }}">
                <div class="sidebar-brand-icon">
                    <!--<i class="fas fa-laugh-wink"></i>-->
                    <img src="{{ url_for('static', filename='img/logo.svg') }}" width="50" height="50" />
                </div>
                <div class="sidebar-brand-text mx-3">Sample App</div>
            </a>

            <!-- Divider -->
            <hr class="sidebar-divider my-0"> 
            {% include 'base/_authorizedPartial.html.j2' %}
            <div class="text-center d-none d-md-inline">
                <button class="rounded-circle border-0" id="sidebarToggle"></button>
            </div>

        </ul>
        <!--End of Sidebar-->
        <div id="content-wrapper" class="d-flex flex-column">
            <!-- Main Content -->
            <div id="content">
                <!-- Topbar -->
                <nav class="navbar navbar-expand navbar-light bg-white topbar mb-4 static-top shadow">

                    <!-- Sidebar Toggle (Topbar) -->
                    <button id="sidebarToggleTop" class="btn btn-link d-md-none rounded-circle mr-3">
                        <i class="fa fa-bars"></i>
                    </button>

                    <!-- Topbar Navbar -->
                    <span class="mr-2 d-none d-md-inline text-current">Sample App</span> 
                    {% include 'base/_loginPartial.html.j2' %}
                </nav>
                <!-- End of Topbar -->
                <!-- Begin Page Content -->
                <div class="container-fluid">
                    {% with messages = get_flashed_messages(with_categories=true) %} 
                        {% if messages %} 
                            {% for category, message in messages %}
                            <div class="alert alert-{{category}} alert-dismissible" role="alert">
                                <button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button> {{ message }}
                            </div>
                            {% endfor %} 
                        {% endif %} 
                    {% endwith %} 
                    {% block content %}{% endblock %}
                </div>
                <!-- /.container-fluid -->

            </div>
            <!-- End of Main Content -->
            <!-- Footer -->
            <footer class="sticky-footer bg-white">
                <div class="container my-auto">
                    <div class="copyright text-center my-auto">
                        <span>Copyright © Sample App 2022</span>
                    </div>
                </div>
            </footer>
            <!-- End of Footer -->
        </div>
    </div>
    <script type="application/javascript" src="{{ url_for('static', filename='node_modules/jquery/dist/jquery.min.js') }}"></script>
    <script type="application/javascript" src="{{ url_for('static', filename='node_modules/bootstrap/dist/js/bootstrap.min.js') }}"></script>
    <script type="application/javascript" src="{{ url_for('static', filename='node_modules/startbootstrap-sb-admin-2/js/sb-admin-2.min.js') }}"></script>
    {% block scripts %}{% endblock %}
    <style>
        body {
            color: #555;
        }
    </style>
</body>

</html>
```
* The base template can be split for better readability and re-usability using the 'include' jinja tag. For example, in the `layoutBase.html.j2` , by using the `{% include 'base/_loginPartial.html.j2' %}` , the template corresponding to the side bar content is rendered from the `_loginPartial.html.j2` file.
```html
<!--templates/base/_loginPartial.html.j2 file-->
<ul class="navbar-nav ml-auto">
    {% if (current_user is defined) and current_user.is_authenticated %}
        <!-- Nav Item - User Information -->
        <li class="nav-item dropdown no-arrow">
            <a class="nav-link dropdown-toggle" href="#" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                <span class="mr-2 d-lg-inline text-gray-600">{{current_user.name}}</span>
            </a>
            <!-- Dropdown - User Information -->
            <div class="dropdown-menu dropdown-menu-right shadow animated--grow-in">
                <a class="dropdown-item" href='#'>
                    <i class="fas fa-user fa-sm fa-fw mr-2 text-gray-400"></i>
                    Profile
                </a>
                <div class="dropdown-divider"></div>
                <a class="dropdown-item" href="#">
                    <i class="fas fa-sign-out-alt fa-sm fa-fw mr-2 text-gray-400"></i>
                    Logout
                </a>
            </div>
        </li>
    {% else %}
        <li class="nav-item">
            <a class="nav-link" href="#">
                <span class="mr-2 d-lg-inline text-gray-600">Login</span>
            </a>
        </li>
    {% endif %}
</ul>
```

```html
<!--templates/base/_authorizedPartial.html.j2 file-->
<!-- Nav Item - Dashboard -->
{% if user %}
    <!-- Nav Item - Dashboard -->
    <li class="nav-item text-uppercase">
        <a class="nav-link" href='#'>
            <i class="fas fa-th-large"></i>
            <span>Web Dashboard</span>
        </a>
    </li>
{% endif %}
<li class="nav-item text-uppercase">
    <a class="nav-link" href="{{ url_for('index') }}">
        <i class="fas fa-eye"></i>
        <span>Page Link</span>
    </a>
</li>
```

### Chile Template
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
* Create a file named `package.json` in the 'static' folder and paste the following in it
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

### References
* official docs - https://jinja.palletsprojects.com/en/3.1.x/templates/#template-inheritance
* 'include' tag in jinja - https://jinja.palletsprojects.com/en/3.1.x/templates/#include
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNjEzNzM5MDQsMTQ4NzY5MjU2NSwtND
QyNjIzMzksMTgyNzc4NzA3NCwtMTUxMjcyNzQwMiw1NzMwODI5
NjQsLTI4OTQ0ODM1NywxMDIzMjkxMDM4XX0=
-->