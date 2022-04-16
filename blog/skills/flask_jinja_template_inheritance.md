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
![sb_admin_template](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/sb_admin_template.png)
## Base Template
* It is just just a jinja template with named blocks in it.
* Child templates can fill the blocks with content
```html
<!--templates/base/layoutBase.html.j2-->
<!DOCTYPE html>
<html lang="en">

<head>
    {% block head %}
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>{% block title %}{% endblock %} - Sample App</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='node_modules/bootstrap/dist/css/bootstrap.min.css') }}" />

    <!-- Custom fonts for sb admin 2-->
    <link href="{{ url_for('static', filename='node_modules/@fortawesome/fontawesome-free/css/all.min.css') | replace('%40', '@')}}" rel="stylesheet" type="text/css">
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
                    <span class="mr-2 d-none d-md-inline text-current">Sample App</span> {% include 'base/_loginPartial.html.j2' %}
                </nav>
                <!-- End of Topbar -->
                <!-- Begin Page Content -->
                <div class="container-fluid">
                    {% with messages = get_flashed_messages(with_categories=true) %} {% if messages %} {% for category, message in messages %}
                    <div class="alert alert-{{category}} alert-dismissible" role="alert">
                        <button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button> {{ message }}
                    </div>
                    {% endfor %} {% endif %} {% endwith %} {% block content %}{% endblock %}
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
    <link href="{{ url_for('static', filename='site.css') }}" rel="stylesheet" type="text/css" /> {% block scripts %}{% endblock %}
    <style>
        body {
            color: #555;
        }
    </style>
</body>

</html>
```


### References
* official docs - https://jinja.palletsprojects.com/en/3.1.x/templates/#template-inheritance
* include in jinja - https://jinja.palletsprojects.com/en/3.1.x/templates/#include
* TODO write about include also
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MDI4NjQ1NTcsLTE1MTI3Mjc0MDIsNT
czMDgyOTY0LC0yODk0NDgzNTcsMTAyMzI5MTAzOF19
-->