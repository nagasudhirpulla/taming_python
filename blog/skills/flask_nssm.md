## Skill - Run a python Flask server as a windows background service using nssm

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)


Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to run a flask server as a background service in windows using nssm

## What is nssm
* nssm runs commands or batch files (in our case, the flask application) as background services in windows
* The services are also restarted in case of failure
* The services can be easily managed using services.msc in windows
* Command line output can be saved in log files as text
* The generated logs can also be rotated based on time and log file size criteria
* nssm also has a graphical editor to manage it's services

### Install nssm in windows
* Download nssm zip file from https://nssm.cc/download and unzip into a folder in C drive
* In the 'Path' system environment variable, add the path of nssm.exe, so that nssm.exe can be recognized in command line

## Example Flask server
The following is an example flask server that we will run as a background service in windows
```py
from flask import Flask
app = Flask(__name__)

@app.route('/')
def index():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=50100, debug=True)
```

### Step 1 : Create a batch file to run the server
* Create a batch file say `run_server.py` that will run the python server in a command line. You can check by running the batch file
```bat
REM run_server.bat
call python server.py
```

### Step 2 : Use nssm to run the batch file as a background service
* Run the following commands to run the batch file as a background service
```bat
call nssm.exe install my_flask_app "%cd%\run_server.bat"
call nssm.exe set my_flask_app AppStdout "%cd%\logs\mis_dashboard.log"
call nssm.exe set my_flask_app AppStderr "%cd%\logs\mis_dashboard.log"
call nssm set my_flask_app AppRotateFiles 1
call nssm set my_flask_app AppRotateOnline 0
call nssm set my_flask_app AppRotateSeconds 86400
call nssm set my_flask_app AppRotateBytes 1048576
call sc start my_flask_app
```
The commands are explained as shown below
* `nssm.exe install my_flask_app "%cd%\run_server.bat"` will create a background service named "my_flask_app" and that runs the command `"%cd%\run_server.bat"`. Here `%cd%` means the 'current directory'
* The below commands will set the file paths to log the output and error streams of 
```bat
call nssm.exe set my_flask_app AppStdout "%cd%\logs\mis_dashboard.log"
call nssm.exe set my_flask_app AppStderr "%cd%\logs\mis_dashboard.log"
```
The above 


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
eyJoaXN0b3J5IjpbLTQ4ODQ3MjE2MCwtOTI0MDUyMzcyLDEzMT
Q3NTI2OV19
-->