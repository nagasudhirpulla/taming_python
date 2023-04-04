## Secure machine to machine communication with OAuth 2.0 Client Credentials flow

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<br>
* In this post we will learn how can we secure machine to machine communication with OAuth 2.0 Client Credentials flow
* We will also demonstrate OAuth 2.0 client credentials flow with keycloak


### Workflow of Client Credentials flow

![oauth_client_credentials_flow.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/oauth_client_credentials_flow.png)
- As a one time activity, the client will be registered in the STS (Secure Token Service or OAuth 2.0 server) with the required API scopes. The client will be authenticated by STS using “client id” and “client secret”
- The client sends “client id” and “client secret” and requests access token from the STS
- The STS validates the client ID and client secret and issues an access token to the client
- The client sends request to resource API with access token attached to the request
- The resource API validates the access token (and client scope if required) and sends the response to the client


## References
- OAuth 2.0 Client credentials flow explained - https://auth0.com/docs/get-started/authentication-and-authorization-flow/client-credentials-flow
- 

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQxOTU2MDE1NywxMTc4OTg3MjkyLC0xMj
Q2MDI4Njg5XX0=
-->