## Skill - Run flask application over HTTPS

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* In this post we will learn how to run a flask application over HTTPS 

## "adhoc" option for testing purposes
```py
from flask import Flask

# create a server instance
app = Flask(__name__)

@app.route('/')
def index():
    return "Hello World!!!"

# run the server
app.run(host="0.0.0.0", port=50100, debug=True, ssl_context="adhoc")
```

* As shown in the above code, add an input `ssl_context="adhoc"` in the `app.run` function. 
* This will run the flask application over HTTPS with a dummy SSL certificate
* This method is very easy and useful for development purposes

### Generate a self-signed SSL certificate using OpenSSL command line utility
* For development purposes, OpenSSL can be used to create a self-signed SSL certificate and generate it's pem and key files using the following command
* OpenSSL for windows can be downloaded from https://slproweb.com/products/Win32OpenSSL.html 
```bash
"C:\Program Files\OpenSSL-Win64\bin\openssl.exe" req -x509 -newkey rsa:4096 -nodes -out cert.pem -keyout key.pem -days 3650
```
* This command generates pem and cert files valid for 3650 days (10 years)
* If git is installed in the windows machine, then openssl.exe can be found at `C:\Program Files\Git\usr\bin\openssl.exe`
```bash
"C:\Program Files\Git\usr\bin\openssl.exe" req -x509 -newkey rsa:4096 -nodes -out cert.pem -keyout key.pem -days 3650
```
Using the above command, openssl in git can be used to generate the self-signed SSL certificate files

## Using .key and .pem files for HTTPS in flask
* key and pem files can be generated from an SSL certificate or generated from a utility like OpenSSL
* pem file is the certificate file and key file is the private key file of the SSL certificate

```py
from flask import Flask

# create a server instance
app = Flask(__name__)

@app.route('/')
def index():
    return "Hello World!!!"

# run the server
app.run(host="0.0.0.0", port=50100, debug=True, ssl_context=('cert.pem', 'key.pem'))
```
* As shown in the above code using `ssl_context=('cert.pem', 'key.pem')` in app.run function can run the application over HTTPS with cert and pem files of the SSL certificate
* If cert and pem files are present in a separate folder say `C:\taming_python\flask_iis`, then 
`ssl_context=('C:\\taming_python\\flask_iis\\cert.pem', 'C:\\taming_python\\flask_iis\\key.pem')` can be used

## Best Practice
* Although we have learnt how to use SSL in flask application, in production scenarios, it is better use SSL in a reverse proxy like Nginx or IIS and place the flask application behind the reverse proxy
* A post on how to host a flask application behind IIS as a reverse proxy can be found [here](https://nagasudhir.blogspot.com/2022/10/iis-as-reverse-proxy-for-python-flask.html) 


## References
* Flask quickstart guide - https://flask.palletsprojects.com/en/2.2.x/quickstart/
* Dowload OpenSSL for windows - https://slproweb.com/products/Win32OpenSSL.html 
* Download git for windows -  
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzIxOTEyMjI0LC05Njc1MjYxMzQsNTkyMT
MzMTMwLDMzMDc5MDg2NCw0NTI5MDY5ODcsLTEzNjIwNDM0MzYs
MTM5MjQ0Njc2MSw0OTkwOTMxNjIsODExOTI2MDE0LDQxMDAzMj
g4XX0=
-->