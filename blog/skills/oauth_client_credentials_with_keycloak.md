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
* In keycloak the well-known endpoint for a realm named "myorg" would be something like "http://localhost:8080/realms/myorg/.well-known/openid-configuration". The well-known URL can be found in the Realm settings page of keycloak
* The well-known URL will return a JSON that contains URLs for various endpoints like certificates, tokens, token revocation etc as shown in the below image

![oauth_well_known_endpoint.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/oauth_well_known_endpoint.png)
### Fetching access_tokens from the token_endpoint
*  Access tokens can be fetched from the token_endpoint URL. The token_endpoint URL can also be found in the well-known URL
* For example, to fetch a token from keycloak realm, say myorg, the token endpoint would be "http://localhost:8080/realms/myorg/protocol/openid-connect/token"
* A POST request should be made to the token_endpoint URL to get the access token. The POST request body should contain the client ID, client secret, grant type (client_credentials) and scope (optional)
* An example request to fetch access token from OAuth server can be
```c
POST http://localhost:8080/realms/myorg/protocol/openid-connect/token
Content-Type:  application/x-www-form-urlencoded

grant_type=client_credentials&client_id=test_api_client&client_secret=zoRdC3erP6p9fci6FgzStDiRlMHkupw6&scope=test_api_access
```



## References
- OAuth 2.0 Client credentials flow explained - https://auth0.com/docs/get-started/authentication-and-authorization-flow/client-credentials-flow
- 

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbNDM4NDk3OTc5LDE4MDg1NTQ3NDMsMTczNj
cwNDU4LDExNzg5ODcyOTIsLTEyNDYwMjg2ODldfQ==
-->