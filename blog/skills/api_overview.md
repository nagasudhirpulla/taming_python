## **What is an API?**

-   API (Application Programming Interface) is a way two applications can talk to each other
-   API is a specification that defines the request and response formats, how to call the server etc.

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/api_simple_sketch.png?raw=true)

## Why APIs

### Modular systems

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/apis%20for%20modular%20systems.png?raw=true)

A system can be developed as modules by different teams instead of a Monolith and modules can communicate with well defined APIs

### Information Hiding

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/apis%20for%20information%20hiding.png?raw=true)

API Client/User need not know the internals.For example, an API server can be developed in Python or Java and client will not know

### Extend applications

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/apis%20for%20extending%20applications.png?raw=true)

A main application can expose API to allow third party developers to create new applications

## **Web API Example**

### **GET Request**

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/api%20get%20request%20example.png?raw=true)

### POST request

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/api%20post%20request%20example.png?raw=true)

## Web API

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/web%20api%20overview.png?raw=true)

Web API is API to communicate with a server over the web/HTTP

## HTTP Protocol

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/http%20protocol%20anatomy.png?raw=true)

HTTP is the protocol used to transfer content over the web

## REST API

REST API is an architectural style that allows clients to communicate with server resources with standard HTTP verbs like GET, POST, PUT, DELETE, HTTP status code for response status, URL parameters for querying etc.

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/rest%20api%20overview.png?raw=true)

## **How to call APIs**

-   Postman – Browser like tool to call web APIs
-   REST Client – Visual Studio Code extension
-   cURL – command line utility
-   Libraries in programming languages – requests module in python, HttpClient class in dotnet, Java

### Postman

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/postman%20overview.png?raw=true)

Postman is a popular to interact with APIs with a convenient UI just like a web browser

### **Visual Studio Code REST Client Extension**

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/api%20post%20request%20example.png?raw=true)

This Visual studio code extension can be used to interact with APIs conveniently in VS code

### cURL command line utility

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/curl%20overview.png?raw=true)

HTTP requests can be done from command line with the cURL command line utility

### Libraries in programming languages

```python
import requests

# POST request form data as a python dictionary
postData = {
    'x': 5,
    'y': 8
}

# Perform HTTP POST request along with post body and get response object in return
resp = requests.post(url='<http://localhost>: 50100/multiply', json=postData)

# check is response status_code is 200
if not resp.ok:
    print("Some unexpected response received...")

# parse the response text as a JSON and get a python dictionary from the response
respData = resp.json()
print(respData)

print(f"The multipication result is {respData["product"]}")

```

-   Libraries like requests module in python, HttpClient in dotnet, Java can be used to easily call APIs from applications

## Hosting APIs

```python
from flask import Flask, request

app = Flask(__name__)

# extract data from post request body
@app.route('/multiply', methods=['POST'])
def multiplyWithPostBody():
    reqJson = request.get_json()
    x = reqJson['x']
    y = reqJson['y']
    prodVal = x * y
    return {"product": prodVal}

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=50100, debug=True)

```

-   Create a program that listens for requests and creates responses as per the API specification
-   A web server can be created to implement Web API server
-   A simple python flask example can be seen above

## **HTTP status codes**

-   Server can set HTTP status codes along with the response body to convey the response outcome
-   Some important and most used HTTP response status codes are



## **API security measures**

### Whitelisting

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/api%20security%20whitelisting.png?raw=true)

### Credentials

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/api%20security%20api%20key.png?raw=true)

### Rate Limiting

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/api%20security%20rate%20limiting.png?raw=true)

### Secure Token Service (STS)

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/STS%20for%20API%20overview.png?raw=true)

-   API Clients and servers are registered in the STS
-   Clients request short-lived tokens for API access
-   API servers validate the tokens for authorization

### **Client Credentials API authorization flow**

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/api%20client%20credentials%20oauth%20overiew.png?raw=true)

In Client Credentials OAuth 2.0 authorization flow, the client application sends its client ID and client secret to the STS, receiving an access token in response. Then the client application uses this access token to access data from the resource server.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU2ODc3MDQ3OF19
-->