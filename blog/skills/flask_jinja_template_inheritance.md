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

## Example Setup
![enter image sb_admin_templatehere](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/sb_admin_template.png)
## Base Template
* It is just just a jinja template with named blocks in it.
* Child templates can fill the blocks with content
```html

```


### References
* official docs - https://jinja.palletsprojects.com/en/3.1.x/templates/#template-inheritance
* include in jinja - https://jinja.palletsprojects.com/en/3.1.x/templates/#include
* TODO write about include also
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMzNjc3OTgzMCwtMTUxMjcyNzQwMiw1Nz
MwODI5NjQsLTI4OTQ0ODM1NywxMDIzMjkxMDM4XX0=
-->