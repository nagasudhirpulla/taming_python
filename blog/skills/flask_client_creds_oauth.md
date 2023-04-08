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
* 

### Fetching access_tokens from the token_endpoint
*  Access tokens can be fetched from the token_endpoint URL. The token_endpoint URL can also be found in the well-known URL
* For example, to fetch a token from keycloak realm, say myorg, the token endpoint would be http://localhost:8080/realms/myorg/protocol/openid-connect/token
* A POST request should be made to the token_endpoint URL to get the access token. The POST request body should contain the client ID, client secret, grant type (client_credentials) and scope (optional). 
* Note that if a scope required by the client application is not a default scope, it should be  explicitly mentioned in the "scope" parameter of the token request POST body. Multiple scopes can be mentioned in the "scope" parameter with spaces in between each scope name.
* An example request to fetch access token from OAuth server can be

```
POST http://localhost:8080/realms/myorg/protocol/openid-connect/token
Content-Type:  application/x-www-form-urlencoded

grant_type=client_credentials&client_id=test_api_client&client_secret=zoRdC3erP6p9fci6FgzStDiRlMHkupw6&scope=test_api_access
```
* The response would be a JSON that contains the access token as shown below. The access token is a string that is generally a JWT (JSON Web Token)
```json
{
  "access_token": "eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJHcm1sZ1JQSUZ1eW4ycldVazl6MW1WdFdLVU1aOFkwTnAxYi12TV8yMkJJIn0.eyJleHAiOjE2ODA1OTk2OTEsImlhdCI6MTY4MDU5OTM5MSwianRpIjoiOTkwMDU0ZTQtM2UzNS00ODI1LTllMDItNmMzZDZjZWZiZTQzIiwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo4MDgwL3JlYWxtcy9teW9yZyIsImF1ZCI6ImFjY291bnQiLCJzdWIiOiI0NmQyZTg4OS0yYmFjLTQ5ZjYtOThmOS1lYjVkMzhmNjhmZjgiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJ0ZXN0X2FwaV9jbGllbnQiLCJhY3IiOiIxIiwiYWxsb3dlZC1vcmlnaW5zIjpbIi8qIl0sInJlYWxtX2FjY2VzcyI6eyJyb2xlcyI6WyJvZmZsaW5lX2FjY2VzcyIsImRlZmF1bHQtcm9sZXMtbXlvcmciLCJ1bWFfYXV0aG9yaXphdGlvbiJdfSwicmVzb3VyY2VfYWNjZXNzIjp7InRlc3RfYXBpX2NsaWVudCI6eyJyb2xlcyI6WyJ1bWFfcHJvdGVjdGlvbiJdfSwiYWNjb3VudCI6eyJyb2xlcyI6WyJtYW5hZ2UtYWNjb3VudCIsIm1hbmFnZS1hY2NvdW50LWxpbmtzIiwidmlldy1wcm9maWxlIl19fSwic2NvcGUiOiJwcm9maWxlIGVtYWlsIHRlc3RfYXBpX2FjY2VzcyIsImNsaWVudEhvc3QiOiIxMjcuMC4wLjEiLCJjbGllbnRJZCI6InRlc3RfYXBpX2NsaWVudCIsImVtYWlsX3ZlcmlmaWVkIjpmYWxzZSwicHJlZmVycmVkX3VzZXJuYW1lIjoic2VydmljZS1hY2NvdW50LXRlc3RfYXBpX2NsaWVudCIsImNsaWVudEFkZHJlc3MiOiIxMjcuMC4wLjEifQ.kCHuOR1gK6tuZfWRv-p7baWq0Kc-gLvGYaaxQBKEfE9dG-heEVvelX3vF2b5napIAkP0hCDxrGs0Xh3z2-0xhw7A3coGuNFfFCTzaV3ROg_B97TT3ja4sjIdZuHSPEuWE-ElllnkGL8PncF1t3LuJ7cxKtjVBV_JkBfuBQW_CSPFD1O7bZxZR7ikY4Xg2iYjg3n3sDz7tWND-xi9LbIndDvfnMDIDMsXADWXKFCDPnHUrRts8QJ1nnZu7W2KEuPSf4fUt0GmxSOUNj9jp5BSTh3hRbYls1KHcB6-535q28_jE09LRyaTUYkGCIX3GzSmzc28827Ni5Sh7f0o1fbusg",
  "expires_in": 300,
  "refresh_expires_in": 0,
  "token_type": "Bearer",
  "not-before-policy": 0,
  "scope": "profile email test_api_access"
}
```
* The access token fetched from the token endpoint can be attached in the requests being made to resource server by the client application. The resource server will validate the access token present in the request for authorizing the request from client application.

### Parsing access token as a JWT (JSON Web Token)
* JWT is a string that contains a header, payload (the main JSON) and signature of the payload.
* A very handy tool to validate and visualize JWTs can be found at https://jwt.io/
* The integrity of JWT can be checked by verifying the signature of the payload and matching it with the signature of JWT. If the payload was tampered, the signature of payload and the signature of JWT will not match
* JWT is a string in the format of `<header>.<payload>.<signature>`. The header and payload will be base64 encoded in the JWT string
* The signature of the payload can be derived using the public key of the OAuth server and the signing algorithm defined in the JWT header. 
* For example, consider a JWT access token below:
 
```
eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJHcm1sZ1JQSUZ1eW4ycldVazl6MW1WdFdLVU1aOFkwTnAxYi12TV8yMkJJIn0.eyJleHAiOjE2ODA1OTk2OTEsImlhdCI6MTY4MDU5OTM5MSwianRpIjoiOTkwMDU0ZTQtM2UzNS00ODI1LTllMDItNmMzZDZjZWZiZTQzIiwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo4MDgwL3JlYWxtcy9teW9yZyIsImF1ZCI6ImFjY291bnQiLCJzdWIiOiI0NmQyZTg4OS0yYmFjLTQ5ZjYtOThmOS1lYjVkMzhmNjhmZjgiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJ0ZXN0X2FwaV9jbGllbnQiLCJhY3IiOiIxIiwiYWxsb3dlZC1vcmlnaW5zIjpbIi8qIl0sInJlYWxtX2FjY2VzcyI6eyJyb2xlcyI6WyJvZmZsaW5lX2FjY2VzcyIsImRlZmF1bHQtcm9sZXMtbXlvcmciLCJ1bWFfYXV0aG9yaXphdGlvbiJdfSwicmVzb3VyY2VfYWNjZXNzIjp7InRlc3RfYXBpX2NsaWVudCI6eyJyb2xlcyI6WyJ1bWFfcHJvdGVjdGlvbiJdfSwiYWNjb3VudCI6eyJyb2xlcyI6WyJtYW5hZ2UtYWNjb3VudCIsIm1hbmFnZS1hY2NvdW50LWxpbmtzIiwidmlldy1wcm9maWxlIl19fSwic2NvcGUiOiJwcm9maWxlIGVtYWlsIHRlc3RfYXBpX2FjY2VzcyIsImNsaWVudEhvc3QiOiIxMjcuMC4wLjEiLCJjbGllbnRJZCI6InRlc3RfYXBpX2NsaWVudCIsImVtYWlsX3ZlcmlmaWVkIjpmYWxzZSwicHJlZmVycmVkX3VzZXJuYW1lIjoic2VydmljZS1hY2NvdW50LXRlc3RfYXBpX2NsaWVudCIsImNsaWVudEFkZHJlc3MiOiIxMjcuMC4wLjEifQ.kCHuOR1gK6tuZfWRv-p7baWq0Kc-gLvGYaaxQBKEfE9dG-heEVvelX3vF2b5napIAkP0hCDxrGs0Xh3z2-0xhw7A3coGuNFfFCTzaV3ROg_B97TT3ja4sjIdZuHSPEuWE-ElllnkGL8PncF1t3LuJ7cxKtjVBV_JkBfuBQW_CSPFD1O7bZxZR7ikY4Xg2iYjg3n3sDz7tWND-xi9LbIndDvfnMDIDMsXADWXKFCDPnHUrRts8QJ1nnZu7W2KEuPSf4fUt0GmxSOUNj9jp5BSTh3hRbYls1KHcB6-535q28_jE09LRyaTUYkGCIX3GzSmzc28827Ni5Sh7f0o1fbusg
```
* The header, payload and signature can be derived by splitting the JWT string by "."
* So the header string would be `eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJHcm1sZ1JQSUZ1eW4ycldVazl6MW1WdFdLVU1aOFkwTnAxYi12TV8yMkJJIn0`. The base64 decoded header would be 
```json
{
  "alg": "RS256",
  "typ": "JWT",
  "kid": "GrmlgRPIFuyn2rWUk9z1mVtWKUMZ8Y0Np1b-vM_22BI"
}
```
* The encryption algorithm and public key id of the OAuth server required for verifying the payload signature is present in the header. 
* The payload would be 
```eyJleHAiOjE2ODA1OTk2OTEsImlhdCI6MTY4MDU5OTM5MSwianRpIjoiOTkwMDU0ZTQtM2UzNS00ODI1LTllMDItNmMzZDZjZWZiZTQzIiwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo4MDgwL3JlYWxtcy9teW9yZyIsImF1ZCI6ImFjY291bnQiLCJzdWIiOiI0NmQyZTg4OS0yYmFjLTQ5ZjYtOThmOS1lYjVkMzhmNjhmZjgiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJ0ZXN0X2FwaV9jbGllbnQiLCJhY3IiOiIxIiwiYWxsb3dlZC1vcmlnaW5zIjpbIi8qIl0sInJlYWxtX2FjY2VzcyI6eyJyb2xlcyI6WyJvZmZsaW5lX2FjY2VzcyIsImRlZmF1bHQtcm9sZXMtbXlvcmciLCJ1bWFfYXV0aG9yaXphdGlvbiJdfSwicmVzb3VyY2VfYWNjZXNzIjp7InRlc3RfYXBpX2NsaWVudCI6eyJyb2xlcyI6WyJ1bWFfcHJvdGVjdGlvbiJdfSwiYWNjb3VudCI6eyJyb2xlcyI6WyJtYW5hZ2UtYWNjb3VudCIsIm1hbmFnZS1hY2NvdW50LWxpbmtzIiwidmlldy1wcm9maWxlIl19fSwic2NvcGUiOiJwcm9maWxlIGVtYWlsIHRlc3RfYXBpX2FjY2VzcyIsImNsaWVudEhvc3QiOiIxMjcuMC4wLjEiLCJjbGllbnRJZCI6InRlc3RfYXBpX2NsaWVudCIsImVtYWlsX3ZlcmlmaWVkIjpmYWxzZSwicHJlZmVycmVkX3VzZXJuYW1lIjoic2VydmljZS1hY2NvdW50LXRlc3RfYXBpX2NsaWVudCIsImNsaWVudEFkZHJlc3MiOiIxMjcuMC4wLjEifQ``` 
The base 64 decoded payload would be 
```json
{
  "exp": 1680599691,
  "iat": 1680599391,
  "jti": "990054e4-3e35-4825-9e02-6c3d6cefbe43",
  "iss": "http://localhost:8080/realms/myorg",
  "aud": "account",
  "sub": "46d2e889-2bac-49f6-98f9-eb5d38f68ff8",
  "typ": "Bearer",
  "azp": "test_api_client",
  "acr": "1",
  "allowed-origins": ["/*"],
  "realm_access": {
    "roles": [
      "offline_access",
      "default-roles-myorg",
      "uma_authorization"
    ]
  },
  "resource_access": {
    "test_api_client": {
      "roles": ["uma_protection"]
    },
    "account": {
      "roles": [
        "manage-account",
        "manage-account-links",
        "view-profile"
      ]
    }
  },
  "scope": "profile email test_api_access",
  "clientHost": "127.0.0.1",
  "clientId": "test_api_client",
  "email_verified": false,
  "preferred_username": "service-account-test_api_client",
  "clientAddress": "127.0.0.1"
}
```

### Validating the access token by resource server using JWT signature
* The **integrity** of the access token received for authorization at the resource server can be verified by the JWT signature. The public key URL required for verifying the JWT signature can be found in the "jwks_uri" of the well-known configuration page  
* The **scopes** of the client application requesting authorization can be verified in the "scope" attribute of the access token JWT payload
* The **expiry** of the access token can also be verified using the "exp" attribute of the access token JWT payload
* Once all the validation on access token is completed, the resource server can authorize client application and send the desired response to client application

### Validating the access token using the token introspection endpoint
* Validating the JWT access token using public key is sufficient in most of the cases.
* But for security reasons, if the client application revokes an access token at the OAuth server before expiry, the resource would not know about the token revocation.
* So to accommodate scenarios like token revocation at OAuth server before expiry, the resource server can ask the OAuth server to validate the token using the token introspection endpoint of the OAuth server. The token introspection endpoint URL can be located in the well-known configuration using the "introspection_endpoint" attribute.
* Let us consider an example to demonstrate the above scenario
* Let us assume a token `<access_token>` was issued to a client application and it expires in 5 minutes
* The client application revokes the token using the following POST request to "revocation_endpoint" URL before 5 mins
```
POST http://localhost:8080/realms/myorg/protocol/openid-connect/revoke
Content-Type:  application/x-www-form-urlencoded

client_id=test_api_client&client_secret=zoRdC3erP6p9fci6FgzStDiRlMHkupw6&token_type_hint=access_token&token=<access_token>
```
* The resource server can check the validity of the token using the "introspection_endpoint" as shown below. Notice that for using the introspect endpoint, the resource server should also be registered as a client in the OAuth server
```
POST http://localhost:8080/realms/myorg/protocol/openid-connect/token/introspect
Content-Type:  application/x-www-form-urlencoded

client_id=test_api_resource&client_secret=VA6tB3MBMI2YOrRhOVYM3M80JHfEhLhH&token=<access_token>
```
* If the token is invalid or revoked, the response would be 
```json
{
	"active": false
}
```

### Video
You can see the video on this post [here](https://youtu.be/V4j-cPJxRJs) 

<iframe width="560" height="315" src="https://www.youtube.com/embed/V4j-cPJxRJs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## References
- OAuth 2.0 Client credentials flow explained - https://auth0.com/docs/get-started/authentication-and-authorization-flow/client-credentials-flow
- JWT decoder and verifier online - https://jwt.io 
- Authlib Docs - https://docs.authlib.org/en/latest/#authlib-python-authentication
- 

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbNjg0MjkzNzgzLDEyOTAzMzA4ODcsLTEwNz
AwNTA4OTEsMTc4NDE3NjM4NF19
-->