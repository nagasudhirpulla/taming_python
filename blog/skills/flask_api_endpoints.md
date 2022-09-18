## Skill - Create API endpoints in flask 

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Extract parameters from URL in flask server](https://nagasudhir.blogspot.com/2022/04/extract-parameters-from-url-in-flask.html)


Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to create simple API endpoints in flask

## What is an API endpoint
* An api endpoint is just a URL at which the server listens for HTTP requests and send JSON or CSV or text as a response

### GET requests
```py
from flask import Flask

app = Flask(__name__)

# send json
@app.route('/hello_json')
def helloJson():
    return {'message': 'Hello World!!!'}

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=50100, debug=True)
```
* In the above example, the server serves a JSON when a GET request is made at the route `/hello_json` 

### passing inputs to HTTP API endpoints
Input data can be passed to API endpoints using the following techniques
*   URL segments - example: `abc.com/sum/1/3`
*   Query parameters - example: `abc.com/sum?x=1&y=3`
*   Request Body : example: In request body the following JSON can be present `{"x":1,"y":3}`. Request body cannot be set only for HTTP GET requests

### URL segments example
```py
from flask import Flask

app = Flask(__name__)

# extract data from URL segments and send JSON response
@app.route('/sum/<int:x>/<int:y>')
def sumFromSegments(x: int, y: int):
    numSum = x + y
    return {'x': x, 'y': y, 'sumVal': numSum}

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=50100, debug=True)
```

* In the above example, the API endpoint listening to GET requests at the route `/sum` will extract the integers from URL segments and send the results in a JSON response
* For example, calling `localhost:50100/sum/1/3` will return `{"sumVal": 4, "x": 1, "y": 3}` 
* Notice that flask allows allows to optionally specify the data types of URL segments also

### Query parameters example
```py
from flask import Flask, request

app = Flask(__name__)

# extract data from query parameters, example abc.com?x=2&y=5
@app.route('/sum')
def sumWithQueryParams():
    x = request.args.get('x', 0, type=int)
    y = request.args.get('y', None, type=int)
    sumVal = x + y
    return {'x': x, 'y': y, 'sumVal': sumVal}

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=50100, debug=True)
```

* In the above example, the API endpoint listening to GET requests at the route `/sum` will extract the integers from URL query parameters and send the results in a JSON response
* For example, calling `localhost:50100/sum?x=2&y=5` will return `{"sumVal": 7, "x": 2, "y": 5}` 
* The query parameter named `x` can be extracted from the URL using `request.args.get('x', 0, type=int)`. The second and third optional arguments are for specifying the default value and value type respectively

### Request body example

```py
from flask import Flask, request

app = Flask(__name__)

# extract data from post request body
@app.route('/sum', methods=['POST'])
def sumWithPostBody():
    reqJson = request.get_json()
    x = reqJson['x']
    y = reqJson['y']
    sumVal = x + y
    return {"message": f"sum of {x} and {y} is {sumVal}"}

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=50100, debug=True)
```

* In the above example, the API endpoint listening to POST requests at the route `/sum` will extract the integers from POST request body and send the results in a JSON response
* For example, calling `localhost:50100/sum` with a POST request body of `{}`
* The query parameter named `x` can be extracted from the URL using `request.args.get('x', 0, type=int)`. The second and third optional arguments are for specifying the default value and value type respectively

### generate URLs to flask blueprint routes using "url_for"
```html
<!-- templates/books/list.html file -->
<html>

<h2>List of Books</h2>
<ul>
    <li><a href="{{url_for('.getItem', id=1)}}">Item1</a></li>
</ul>

<a href="{{url_for('index')}}">Back to Home</a>
<br>
<a href="{{url_for('authors.list')}}">Authors</a>
</html>
```
* In the above example, the URL to the flask route function `getItem` within the same blueprint can be generated using `url_for('.getItem', id=1)`. Hence relative URLs with in the same blueprint can be generated using the '.' (dot) notation.
* The URL for flask route function `list` within the blueprint `authors` can be generated using `url_for('authors.list')`
* Hence URLs for routes inside blueprints can be generated using the '.' (dot) notation
* The  URL for the route function 'index' in the main server can be generated using `url_for('index')` 

### Video
The video for this post can be seen [here](https://youtu.be/SezbDCz0Ock)

<iframe width="560" height="315" src="https://www.youtube.com/embed/SezbDCz0Ock" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## References
* Official flask blueprints docs - https://flask.palletsprojects.com/en/latest/blueprints/

<!--stackedit_data:
eyJoaXN0b3J5IjpbNjE3MTU3Nzk1LC0zNDAyMDAwNiw5MjY1NT
c1NjIsLTMxNTg1NzE4MywtMTYyMDA2ODU0Ml19
-->