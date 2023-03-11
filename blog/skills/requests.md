## Skill - Requests module in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision.
<hr>

Using requests module, we can make HTTP requests in our python scripts

## Installation

Requests module can be installed with pip using the following command

```bash
python -m pip install python
```

## Use cases

 There can be many use cases for using requests module like

- access web pages for automating tasks like extracting data, monitoring etc
- access APIs for content like JSON
- download files like images, csv
- send post requests

## Examples

### Load a web page

```python
import requests

# query parameters, the mail URL will be appended with"?client=firefox-b-d&q=taming+python+blog"
urlParams={"client":"firefox-b-d", "q":"taming+python+blog"}

# perform a HTTP GET request and get response object in return
res = requests.get(url="https://www.google.com/search", params=urlParams)

# check the response status code
if not res.status_code == 200:
    print("The page is not accessible😒")
    quit()

# get the page load time
print(f"The page took {res.elapsed.total_seconds()} seconds to load")

# get the response text length
print(f"The HTML in page response is {len(res.text)} characters long")
```

- In the above example, we are performing a google search with python by doing a HTTP GET request
- The "params" input to requests.get function is a convenient way to add query parameters to URLs. In this example, the GET request would be sent to the URL “https://www.google.com/search?client=firefox-b-d&q=taming+python+blog”
- The status code in the response object can be checked before processing the response
- The page load time can be accessed with the “elapsed” property of the response object
- The response text can be read using the “text” attribute of the response object

### Download a file

```python
import requests

# perform a HTTP GET request along with request headers and get the response object in return
# The request headers are provided as a python dictionary
res = requests.get(url="https://httpbin.org/image",
                   headers={"accept": "image/webp"})

# Check the response status code
if not res.status_code == 200:
    print("Could not download the image...")
    quit()

# Save the response as an image file
open("test.png", 'wb').write(res.content)
```

- In the above example, an image is downloaded from a URL using a HTTP GET request
- Additional request headers are provided as a dictionary along with the request using the “headers” input
- The file can be saved using the “content” attribute of the response which reads the response contents as bytes

### HTTP POST request

```python
import requests

# POST request form data as a python dictionary
postData = {
    'name': 'abcd',
    'dob': '2020-12-30'
}

# Perform HTTP POST request along with post body and get response object in return
resp = requests.post(url='https://httpbin.org/post',
                     data=postData)

# check is response status_code is 200
if not resp.ok:
    print("Some unexpected response received...")

# parse the response text as a JSON and get a python dictionary from the response
respData = resp.json()
print(respData)
```

- In the above example, a HTTP POST request is made along with POST request body as a python dictionary
- The response text can be easily parsed into JSON if required by calling the “.json()” method on the response object

### Basic Authorization

```python
import requests

# perform a HTTP GET request along with request headers 
# and authorization header based on the username and password provided to the "auth" parameter
res = requests.get(url="https://httpbin.org/basic-auth/abcd/pwd",
                   headers={"accept":"application/json"},
                   auth=("abcd", "pwds"))

if res.status_code == 401:
    print("Wrong credentials...")
    quit()

if not res.status_code == 200:
    print("Got some unexpected response...")
    quit()

print(res.json())
```

- In the above example, a HTTP GET request is made along with basic authentication
- By providing username and password as a tuple to the “auth" parameter, a request header named “Authorization” will be set appropriately

### Fetch data from JSON API

```python
import requests
githubUname = "dotnet"

# get data from URL and create a response object
res = requests.get(url=f"https://api.github.com/users/{githubUname}/repos")

# check the response status code if request succeded
if not res.status_code == 200:
    print("could not fetch the data :-(")
    quit()

# get time period to get the data
fetchPeriod = res.elapsed
print(f"Data waas fetched in {fetchPeriod.total_seconds()} seconds")

# parse json from the response as a list of python dictionary.
# If required, the response can be read as a string using res.text
repoObjs = res.json()

maxStarsRepo = max(repoObjs, key=lambda x: x["stargazers_count"])
print(f"The repo with maximum stars is {maxStarsRepo['name']}")

print(f"The repos of the user {githubUname} are ", end="")
print(", ".join([x["name"] for x in repoObjs]))

print("execution complete...")
```

- In the above example, a GET request is made to an API to fetch JSON response
- The response is parsed and some insights are derived by processing the response content

#### Video
The video tutorial for this post can be found [here](https://youtu.be/gtfEZr6wK5E)

<iframe width="560" height="315" src="https://www.youtube.com/embed/gtfEZr6wK5E" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## References

- official docs - [https://requests.readthedocs.io/en/latest/](https://requests.readthedocs.io/en/latest/)
- requests module authentication guides - [https://requests.readthedocs.io/en/latest/user/authentication/](https://requests.readthedocs.io/en/latest/user/authentication/)


<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgzODUyMjA2NiwtMjAyNzQxNDc3Ml19
-->