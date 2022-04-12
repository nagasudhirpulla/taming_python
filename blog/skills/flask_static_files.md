## Skill - Serve static files in flask

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* Static files can be files like images, PDFs etc. that can be stored in the server folder and displayed or downloaded in the browser

## hosting static files
* Static files can be stored in a folder named "static" in the same folder as the server python file
* All static files can be accessible without any authorization, so do not host sensitive data in static folder
* URL for a static file can be generated dynamically without hard-coding using the `url_for` function. Example: url_for('static', 'img/abcd.png')
* `url_for` can be used directly in jinja template like `{{ url_for('static', 'img/abcd.png') }}`. For using `url_for` function in python code, we need to import it from flask module like `from flask import url_for`
```html
<html>

<body>
    <a target="_blank" href="{{ url_for('static', filename='img/abcd.png') }}">Download Image</a>
    <br/>
    <button>Dummy Button</button>
</body>

</html>
```

### References
* https://stackoverflow.com/questions/20646822/how-to-serve-static-files-in-flask
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQzNjI0NTk1MCwxOTA2ODI4MjgsOTgzNz
YxMzQ3XX0=
-->