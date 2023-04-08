## Implement python client and flask server for OAuth 2.0 client credentials flow

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
-   [OAuth 2.0 for centralized Authorization and Authentication of users and applications](https://nagasudhir.blogspot.com/2023/03/oauth-20-for-centralized-authorization.html)
- [Setup Keycloak as OAuth 2.0 server in Windows for testing and development](https://nagasudhir.blogspot.com/2023/04/setup-keycloak-as-oauth-20-server-in.html)
- [Secure machine to machine communication with OAuth 2.0 Client Credentials flow](https://nagasudhir.blogspot.com/2023/04/secure-machine-to-machine-communication.html)

<br>

* In this post we will learn how to create a client and flask server for client credentials flow based authorization


### Workflow of Client Credentials flow
![oauth_client_credentials_flow.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/oauth_client_credentials_flow.png)
- This the workflow of client credentials flow in OAuth 2.0
- A complete blog post explaining this workflow can be found [here](https://nagasudhir.blogspot.com/2023/04/secure-machine-to-machine-communication.html)

## The OAuth server 
For this demo, we will run a Keycloak server as an OAuth server and register the client application in it. The following are the steps to register a client
* Create a realm named "myorg" in keycloak
* Create a client scope named "test_api_access"
* Create a client with client_id "test_api_client". Keep Client authentication as "ON" and Authentication flow as only "Service accounts roles". This will set the client application authorization flow as client credentials flow.

![keycloak_client_credentials_settings.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/keycloak_client_credentials_settings.png)
* In the client scopes tab of the client, add the scope "test_api_access". If the scope is made optional, the access token will include this scope only if explicitly requested by the client application 
 
## The Python client
* In this demo, a python script will act as a client and fetch data from the resource server
* `requests` python module is used to fetch access token from the OAuth server and data from resource server using HTTP GET and POST requests. It can be installed using the command `pyhon -m pip install requests`
* The following is the workflow of the python client
	* Fetch access token from OAuth server by providing client credentials
	* Perform data request to resource server URL by including the access token in the "Authorization" header of the request

```py
# client.py
import requests

tokenUrl = "http://localhost:8080/realms/myorg/protocol/openid-connect/token"

client_id = "test_api_client"
client_secret = "fsQJIcU3Ze3ymaYSA6cxlHVIw0LDIDeY"
requiredScopes = " ".join(["test_api_access"])

# request the access token from OAuth server
post_body = {"grant_type": "client_credentials",
             "client_id": client_id,
             "client_secret": client_secret,
             "scope": requiredScopes}
headers = {'content-type': "application/x-www-form-urlencoded"}

accessTokenResp = requests.post(tokenUrl,
                    data=post_body,
                    headers=headers)

# derive the access token from OAuth server response
if not accessTokenResp.ok:
    print("server token response status not ok")
    quit()

accessTokenRespJson = accessTokenResp.json()

if not "access_token" in accessTokenRespJson:
    print("access_token not found in token response")
    quit()

accessToken = accessTokenRespJson["access_token"]
print(accessToken)

# request data from resource server with access token in the request header
apiReqHeaders = {
    'content-type': "application/json",
    'authorization': f"Bearer {accessToken}"
}
apiResp = requests.get(
    "http://localhost:50100/api/private-scoped", headers=apiReqHeaders)

# parse the response from resource server
if not apiResp.ok:
    print("ok response not received from resource API call")
    quit()

print("printing API response...")
print(apiResp.json())
print("execution complete!")

```

## The Resource server
* For this demo, a flask server will be the resource server 
* Some endpoints will be authorize requests using the client credentials flow
* A flask decorator that acts as a request middle-ware will be used to add authorization to the flask server endpoint. So just by adding the decorator, authorization can be added to the flask endpoint
* The decorator for authorizing the request is created using the `authlib` python module. It can be installed using the command `python -m pip install Authlib`
* The workflow of the request authorization in resource server is as follows:
	* Extract the access token from request authorization header
	* Fetch the public key from OAuth server for verifying the access token JWT signature
	*  Validate the JWT signature, expiration time, scope etc. If all the criteria are satisfied, then authorize the request

```py
# server.py
import json
from urllib.request import urlopen
from authlib.integrations.flask_oauth2 import ResourceProtector
from authlib.jose.rfc7517.jwk import JsonWebKey
from authlib.oauth2.rfc7523 import JWTBearerTokenValidator
from flask import Flask, jsonify

class ClientCredsTokenValidator(JWTBearerTokenValidator):
    def __init__(self, issuer):
        jsonurl = urlopen(f"{issuer}/protocol/openid-connect/certs")
        public_key = JsonWebKey.import_key_set(
            json.loads(jsonurl.read())
        )
        super(ClientCredsTokenValidator, self).__init__(
            public_key
        )
        self.claims_options = {
            "exp": {"essential": True},
            "iss": {"essential": True, "value": issuer}
        }

require_auth = ResourceProtector()
validator = ClientCredsTokenValidator("http://localhost:8080/realms/myorg")
require_auth.register_token_validator(validator)

APP = Flask(__name__)

@APP.route("/api/public")
def public():
    """No access token required."""
    response = (
        "No need of Authorization to see this"
    )
    return jsonify(message=response)

@APP.route("/api/private")
@require_auth(None)
def private():
    """A valid access token is required."""
    response = (
        "Authorization is required to see this"
    )
    return jsonify(message=response)

@APP.route("/api/private-scoped")
@require_auth("test_api_access")
def private_scoped():
    """A valid access token and scope are required."""
    response = (
        "Authorization with a scope named test_api_access is required to see this"
    )
    return jsonify(message=response)

APP.run(host="0.0.0.0", port=50100, debug=True)

```

* As shown in the above example, the decorator `require_auth` for authorizing the requests based on client credentials flow is created very easily using the `ResourceProtector` and `JWTBearerTokenValidator` classes of `authlib` python module
* `@require_auth(None)` means, no specific scopes are required for authorization
* `@require_auth("test_api_access")` means, a scope named "test_api_access" is required for authorizing the request
* `@require_auth(["test_api_access", "email"])` means, both the scopes "test_api_access" and "email" are required for authorizing the request

## Running the demo
* Run the Keycloak server with the required realm, client, client credentials and client scope
* Run the flask resource server
* Run the client script
* If the client gets authorized the resource server, the result will be printed in the console without any errors

## Implementing own jwt validation flask decorator using pyjwt
* authlib python module uses pyjwt under the hood to implement the access token validation flask decorator
* A JWT validation flask decorator from scratch can also be created as shown below.
* However we do not recommend this approach unless required since the authlib implementation of JWT validation decorator is more robust and less error prone
* `pyjwt` python module can be installed us

```py	
# authdecorator.py
import json
from functools import wraps
import jwt
import requests
from flask import abort, request

def requireClientCredsDecoratorFactory(issuer=None):
    def req_client_creds(scopes=None):
        def decorator(f):
            @wraps(f)
            def decorated_function(*args, **kwargs):
                # print(f"Decorator hit with scopes as {scopes}...")
                # read access token from bearer token of authorization header
                accessToken = request.headers.get(
                    'Authorization', "").replace("Bearer ", "")

                if accessToken == "":
                    abort(401)

                # read the jwt header and derive algorithm and keyId for jwt validation
                jwtHeader = jwt.get_unverified_header(accessToken)
                jwtAlg = jwtHeader['alg']
                keyId = jwtHeader['kid']

                # fetch required public key for jwt validation
                pubKeysUrl = f"{issuer}/protocol/openid-connect/certs"
                allPubKeys = requests.get(pubKeysUrl).json()["keys"]
                reqPubKeyJwk = [x for x in allPubKeys if x["kid"] == keyId][0]
                reqPubKey = jwt.algorithms.RSAAlgorithm.from_jwk(
                    json.dumps(reqPubKeyJwk))

                # validate jwt payload
                # jwt.decode also validates the audience and expiry time
                # https://pyjwt.readthedocs.io/en/latest/api.html#jwt.decode
                jwtPayload = jwt.decode(
                    accessToken,
                    key=reqPubKey,
                    algorithms=[jwtAlg, ],
                    options={"verify_aud":False}
                )

                # validate client scopes for authorization
                # derive the required scopes for authorization
                reqScopes = []
                if isinstance(scopes, str):
                    reqScopes = scopes.split(" ")
                elif isinstance(scopes, list):
                    reqScopes = scopes

                if len(reqScopes) > 0:
                    jwtScopes = jwtPayload["scope"].split(" ")
                    isAnyReqScopeAbsent = len(
                        [x for x in reqScopes if x not in jwtScopes]) > 0
                    if isAnyReqScopeAbsent:
                        abort(401)
                return f(*args, **kwargs)
            return decorated_function
        return decorator
    return req_client_creds

```  

* In the above example, a flask decorator that validates and authorizes access token is created using the `pyjwt` module

## References
- OAuth 2.0 Client credentials flow explained - https://auth0.com/docs/get-started/authentication-and-authorization-flow/client-credentials-flow
- JWT decoder and verifier online - https://jwt.io 
- Authlib Docs - https://docs.authlib.org/en/latest/#authlib-python-authentication
- pyjwt docs - https://pyjwt.readthedocs.io/en/latest/api.html#jwt.decode
- 

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbOTI1NTUwODksMTI5MDMzMDg4NywtMTA3MD
A1MDg5MSwxNzg0MTc2Mzg0XX0=
-->