## Skill - Create API endpoints in flask 

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Extract parameters from URL in flask server](https://nagasudhir.blogspot.com/2022/04/extract-parameters-from-url-in-flask.html)
* [Forms with front-end and server-side validation in Flask web applications](https://nagasudhir.blogspot.com/2022/06/forms-with-front-end-and-server-side.html)


Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to create simple API endpoints in flask

## What is an API endpoint
* An api endpoint is just a route at which the server listens for HTTP requests and send JSON or CSV or text as a response

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

### Passing inputs to HTTP API endpoints
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

* In the above example, the API endpoint listening to POST requests at the route `/sum` will extract the integers from POST request JSON body and send the results in a JSON response
* For example, calling `localhost:50100/sum` with a POST request body of `{"x":1, "y":4}` will return a response `{"message": "sum of 1 and 4 is 5"}`
* Request body cannot be set for HTTP GET requests
* Hence this request cannot be made directly from a browser. Instead tools like POSTMAN or REST Client extension in visual studio code can be used to easily send requests other than HTTP GET requests

![api_endpoint_http_post_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/api_endpoint_http_post_demo.png)
### Choice of HTTP methods/verbs for API endpoints as per REST conventions
* The HTTP request methods of API end points can be any one of GET, POST, PUT, DELETE
* The HTTP request method/verb of the API endpoint can be decided according to the action performed by the API endpoint as shown below   
	* GET - querying stuff - example: get list of users	
	* POST - for giving commands/creating something - example: create a person
	* PUT - for modify/edit command - example: change the name of the user
	* DELETE - for delete command - example: delete a user

### HTTP status codes in responses
To convey the type of response, the end point can set HTTP status codes along with the response body. Some important and most used HTTP response status codes are

-   200 OK
-   201 Created
-   204 No Content
-   301 Moved Permanently
-   400 Bad Request
-   401 Unauthorized
-   404 Not Found
-   403 Forbidden
-   409 Conflict
-   500 Internal Server Error 

The following is an example API end point that sends errors in responses
```py
from flask import Flask, request

app = Flask(__name__)

# extract data from post request body
@app.route('/divide', methods=['POST'])
def sumWithPostBody():
    reqJson = request.get_json()
    x = reqJson['x']
    y = reqJson['y']
    try:
        result = x/y
        return {"message": f"{x} divided by {y} is {result}"}
    except Exception as err:
        return {"error": str(err)}, 400

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=50100, debug=True)
```
![api_endpoint_http_error_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/api_endpoint_http_error_demo.png)
* Here we sent status code of 400 for wrong user input
* If we want to convey authorization failure, we can send status code 401 and so on

### Video
The video for this post can be seen [here](https://youtu.be/duE5P1hG6sg)

<iframe width="560" height="315" src="https://www.youtube.com/embed/duE5P1hG6sg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## References
* Flask quickstart guide - https://flask.palletsprojects.com/en/2.2.x/quickstart/


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzODgxNTY0OThdfQ==
-->