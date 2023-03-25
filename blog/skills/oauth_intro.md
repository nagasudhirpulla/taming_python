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

### References
* Official guide - https://matplotlib.org/3.1.1/gallery/ticks_and_spines/tick-locators.html
* Official documentation - https://matplotlib.org/3.1.1/api/ticker_api.html#tick-locating
* another post - https://jakevdp.github.io/PythonDataScienceHandbook/04.10-customizing-ticks.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQzODQyMDgxMiw2NTM3MTMxMTEsLTk4MT
Y0NzQzOSwtMjA5Njg5NDU0OV19
-->