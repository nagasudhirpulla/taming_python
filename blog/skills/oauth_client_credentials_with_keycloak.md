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
#### The "well-known" configuration endpoint
* To get the STS URLs for various tasks like getting public keys, fetching, validating, revoking token, verifying tokens etc., the STS provides a URL called "well-known" URL as per the OAuth 2.0 specification
* In keycloak the well-known endpoint for a realm named "myorg" would be something like http://localhost:8080/realms/myorg/.well-known/openid-configuration . The well-known URL can be found in the Realm settings page of keycloak
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
* The response would be a JSON that contains the access token as shown below
* The access token is a string that is generally a JWT (JSON Web Token)
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

### Access Token as a JWT (JSON Web Token)
* JWT is a string that contains a header, payload (the message) and hash  


## References
- OAuth 2.0 Client credentials flow explained - https://auth0.com/docs/get-started/authentication-and-authorization-flow/client-credentials-flow
- 

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMTc2NjQ2MzQsLTEzOTUxNzc5ODksMT
gwODU1NDc0MywxNzM2NzA0NTgsMTE3ODk4NzI5MiwtMTI0NjAy
ODY4OV19
-->