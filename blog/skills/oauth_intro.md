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
* To support multiple scenarios like machine-to-machine, backend

### References


<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ1Mzk0MDE4LDY1MDYxNDc2NywxMTIxOD
U3Nzc2LDY1MzcxMzExMSwtOTgxNjQ3NDM5LC0yMDk2ODk0NTQ5
XX0=
-->