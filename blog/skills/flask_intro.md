
## Skill - Flask python module for building web servers

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* **flask** is a python library for creating web applications.
* It is easy and quick to learn flask

## Use cases
* Simple web interfaces for python applications can be build very quickly using flask
* flask can be used to create HTTP services or applications that require python modules like pandas, numpy etc

## Installing Flask
Install flask using pip with the following command
```
python -m pip install flask
```

## Simple Flask server
```python
from flask import Flask

# create a flask server
app = Flask(__name__)

# just return 'Hello World!' text when the route '/' is called
@app.route('/')
def index():
    return 'Hello, World!'

# __name__ will be __main__ only if this file is the entry point
if __name__ == '__main__':
    # run the server on this ip and port 50100
    app.run(host='0.0.0.0', port=50100, debug=True)
```
* In above example, the index function is assigned a route at '/' using 

## References
* Flask quickstart - https://flask.palletsprojects.com/en/2.1.x/quickstart/
* 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM3MTE1OTA4MywyNTYwNTMwNzUsMTU0Nz
Y5NTE1OCw2NDY5OTgwMTZdfQ==
-->