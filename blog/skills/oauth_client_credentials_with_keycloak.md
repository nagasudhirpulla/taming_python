## Secure machine to machine communication with OAuth 2.0 Client Credentials flow

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<br>
* In this post we will learn how can we secure machine to machine communication with OAuth 2.0 Client Credentials flow
* We will also demonstrate OAuth 2.0 client credentials flow with keycloak


### Workflow of Client Credentials flow

![oauth_client_credentials_flow.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/oauth_client_credentials_flow.png)
- As a one time activity, the client application will be registered in the STS (Secure Token Service or OAuth 2.0 server) with the required API scopes. The client will be given “client id” and “client secret” by the STS
- Step 1 - The client sends “client id” and “client secret” and requests access token from the STS
- Step 2 - The STS validates the client ID and client secret and issues an access token to the client
- Step 3 - The client sends request to resource API with access token attached to the request
- Step 4 - The resource API validates the access token (and the client scopes if required) and sends the response to the client

### Implementation of client credentials flow
### Creating a client in keycloak for demo
* Create a realm named "myorg" in keycloak
* Create a client scope named "test_api_access"
* Create a client with client_id "test_api_client". Keep Client authentication as "ON" and Authentication flow as only "Service accounts roles". This will set the client application authorization flow as client credentials flow.

![keycloak_client_credentials_settings.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/keycloak_client_credentials_settings.png)
* In the client scopes tab of the client, add the scope "test_api_access". If the scope is made optional, the access token will include this scope only if explicitly requested by the client application 
 
#### The "well-known" configuration endpoint
* To get the STS URLs for various tasks like getting public keys, fetching, validating, revoking, verifying tokens etc., the STS provides a URL called "well-known" URL as per the OAuth 2.0 specification
* In keycloak, the well-known endpoint for a realm named "myorg" would be something like http://localhost:8080/realms/myorg/.well-known/openid-configuration . The well-known URL can also be found in the Realm settings page of keycloak
* The well-known URL will return a JSON that contains URLs for various endpoints like certificates, tokens, token revocation etc as shown in the below image

![oauth_well_known_endpoint.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/oauth_well_known_endpoint.png)
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
* The integrity of JWT can be checked by verifying the signature of the payload and matching it with the signature of JWT. If the payload was tampered, the signature of payload and the hash of JWT will not match
* JWT is a string in the format of `<header>.<payload>.<signature>`. The header and payload will be base64 encoded in the JWT string
* The signature of the payload can be derived using the public key of the OAuth 2.0 server and the signing algorithm defined in the JWT header. 
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
* The encryption algorithm and public key id of the OAuth 2.0 server required for verifying the payload signature is present in the header. 
* The payload would be `eyJleHAiOjE2ODA1OTk2OTEsImlhdCI6MTY4MDU5OTM5MSwianRpIjoiOTkwMDU0ZTQtM2UzNS00ODI1LTllMDItNmMzZDZjZWZiZTQzIiwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo4MDgwL3JlYWxtcy9teW9yZyIsImF1ZCI6ImFjY291bnQiLCJzdWIiOiI0NmQyZTg4OS0yYmFjLTQ5ZjYtOThmOS1lYjVkMzhmNjhmZjgiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJ0ZXN0X2FwaV9jbGllbnQiLCJhY3IiOiIxIiwiYWxsb3dlZC1vcmlnaW5zIjpbIi8qIl0sInJlYWxtX2FjY2VzcyI6eyJyb2xlcyI6WyJvZmZsaW5lX2FjY2VzcyIsImRlZmF1bHQtcm9sZXMtbXlvcmciLCJ1bWFfYXV0aG9yaXphdGlvbiJdfSwicmVzb3VyY2VfYWNjZXNzIjp7InRlc3RfYXBpX2NsaWVudCI6eyJyb2xlcyI6WyJ1bWFfcHJvdGVjdGlvbiJdfSwiYWNjb3VudCI6eyJyb2xlcyI6WyJtYW5hZ2UtYWNjb3VudCIsIm1hbmFnZS1hY2NvdW50LWxpbmtzIiwidmlldy1wcm9maWxlIl19fSwic2NvcGUiOiJwcm9maWxlIGVtYWlsIHRlc3RfYXBpX2FjY2VzcyIsImNsaWVudEhvc3QiOiIxMjcuMC4wLjEiLCJjbGllbnRJZCI6InRlc3RfYXBpX2NsaWVudCIsImVtYWlsX3ZlcmlmaWVkIjpmYWxzZSwicHJlZmVycmVkX3VzZXJuYW1lIjoic2VydmljZS1hY2NvdW50LXRlc3RfYXBpX2NsaWVudCIsImNsaWVudEFkZHJlc3MiOiIxMjcuMC4wLjEifQ`. The base 64 decoded payload would be 
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

### Validating the access token using token introspection endpoint
* Validating the JWT access token using public key is sufficient in most of the cases.
* But for security reasons, if the client application revokes an access token at the OAuth server before expiry, the resource would not know about the token revocation.
* So to accommodate scenarios like token revocation at OAuth server before expiry, the resource server can ask the OAuth server to validate the token using the token introspection endpoint of the OAuth server. The token introspection endpoint URL can be located in the well-known configuration using the "introspection_endpoint" attribute.
* Let us consider and example to demonstrate the above scenario
* Let us assume a token `<access_token>` was issued to a client application and it expires in 5 minutes
* The client application revokes the token using the following POST request to "revocation_endpoint" URL before 5 mins
```
POST http://localhost:8080/realms/myorg/protocol/openid-connect/revoke
Content-Type:  application/x-www-form-urlencoded

client_id=test_api_client&client_secret=zoRdC3erP6p9fci6FgzStDiRlMHkupw6&token_type_hint=access_token&token=<access_token>
```
* 

## References
- OAuth 2.0 Client credentials flow explained - https://auth0.com/docs/get-started/authentication-and-authorization-flow/client-credentials-flow
- JWT decoder and verifier online - https://jwt.io 

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMjM0MzE0MDUsMTUxNzA1NjcyMCwtMT
I4NTU4NTE3MSwtMTkxMTExMDg4LC05MDA0MzQ2NDYsLTM2MzA5
MDA1NSw3NjE0OTE4NTksMTMzMzQyNTEwMywtMTM5NTE3Nzk4OS
wxODA4NTU0NzQzLDE3MzY3MDQ1OCwxMTc4OTg3MjkyLC0xMjQ2
MDI4Njg5XX0=
-->