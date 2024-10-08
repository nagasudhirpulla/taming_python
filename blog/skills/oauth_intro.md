## Skill - OAuth 2.0 for centralized Authorization and Authentication of users and applications

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

## What is OAuth 2.0
![OAuth_2_big_picture.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/OAuth_2_big_picture.png)
- Using OAuth 2.0 specification, applications can trust a central server for authorizing and authenticating users or applications
- The identity and access rights information of users or applications will be centrally stored in the identity server / Secure Token Service (STS)
- Identity server can authenticate users or applications and issue tokens to them for getting access to the secured resources in the resource server
- Since user or application gets authenticated at an identity server for getting access to resources in one or multiple resource servers, Single-Sign-On (SSO) is implementable using OAuth 2.0 and users or applications identity and access information can be centrally managed.
- OpenID connect is a layer on top of OAuth 2.0 for facilitating authentication and user information retrieval to client applications 

## OAuth 2.0 Terminology
![OAuth_2_Terminology.png](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/OAuth_2_Terminology.png)
### Identity Server / Secure Token Server (STS)
A software that issues token to clients for accessing resources

### User
A human trying to access the resources using a registered client

### Client
A software registered in the Identity server that can request tokens from the Identity Server for authenticating users (requires identity token) or accessing resources (requires access token)

### Resources
Resources are the data protected by the Identity Server. The data can be identity data (username, email, phone number etc. also called as **user claims**) or APIs

### Identity Token
Identity token is issued by the STS to the client after authenticating a user. It contains user identifier information (subject claim) and how and when the user is authenticated. It may also contain additional user identity information in it.

### Access Token
Access token are issued to clients by the STS for accessing resources. They contain information about the client and user (if present). APIs use these tokens to validate the access of clients

## OAuth 2.0 Flows
* OAuth 2.0 Flow is the process of authorizing or authenticating a user or application. 
* There are multiple flows in OAuth 2.0 specification as listed below to support scenarios like machine-to-machine, back-end web applications, Single Page Apps (SPAs), input constrained devices etc.
	* Authorization Code Flow
	* Authorization Code Flow with Proof Key for Code Exchange (PKCE)
	* Implicit Flow with Form Post
	* Hybrid Flow
	* Client Credentials Flow
	* Device Authorization Flow
	* Resource Owner Password Flow

## OAuth 2.0 implementation

### OAuth 2.0 Server
* [Keycloak](https://www.keycloak.org) is an open-source Identity and Access Management (IAM) solution by RedHat that can be used as an OAuth 2.0 server. It also provides a UI for managing users, clients and resources
* Many providers like Okta also provide OAuth 2.0 services in the cloud

### OAuth 2.0 client and Resource Server 
* OAuth 2.0 authorization and authentication can be integrated in applications using many opensource frameworks in various languages like authlilb in python, ASP.NET Core Identity, IdentityModel in dotnet

### Video
You can see the video on this post [here](https://youtu.be/W7yeiglv9mI) 

<iframe width="560" height="315" src="https://www.youtube.com/embed/W7yeiglv9mI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

### References
* Terminology in OAuth 2.0 - https://identityserver4.readthedocs.io/en/latest/intro/terminology.html
* Overview of different OAuth 2.0 flows - https://auth0.com/docs/get-started/authentication-and-authorization-flow

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMDE4OTczOTgsLTk5Nzk5MDIwMiw0ND
YwNTkzNzQsMTk5OTA1NDg5MCw2NTA2MTQ3NjcsMTEyMTg1Nzc3
Niw2NTM3MTMxMTEsLTk4MTY0NzQzOSwtMjA5Njg5NDU0OV19
-->