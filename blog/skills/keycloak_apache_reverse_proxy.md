
# Apache as reverse proxy for keycloak 

* A reverse proxy like Apache can be used with Keycloak
* A reverse proxy sits in between the clients and server and forwards the client requests to the server

![keycloak_apache_architecture.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_apache_architecture.png?raw=true?raw=true)

## Keycloak configuration for running behind Reverse Proxy

### Reverse Proxy Mode - Edge
* We will use "edge" mode or SSL Termination mode of Reverse Proxy for this scenario.
* The requests would be in HTTPS till Apache server (Reverse Proxy) and Apache will send HTTP requests to Keycloak

![keycloak_edge_mode_proxy.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_edge_mode_proxy.png?raw=true)
### Other Reverse Proxy Modes
* In Passthrough mode, HTTPS connections from clients are passed to keycloak directly without SSL termination at Reverse Proxy
* In Reencypt mode, clients connect to Reverse Proxy via HTTPS and reverse proxy also connects to Keycloak via HTTPS. Hence SSL certificates are needed to be configured in both Reverse Proxy and Keycloak  

```bash
# The file path to a server certificate or certificate chain in PEM format.
https-certificate-file=${kc.home.dir}/conf/kc.crt.pem

# The file path to a private key in PEM format.
https-certificate-key-file=${kc.home.dir}/conf/kc.key.pem

# The proxy address forwarding mode if the server is behind a reverse proxy.
#proxy=edge

# The proxy headers that should be accepted by the server
proxy-headers=xforwarded

# Hostname for the Keycloak server.
# hostname=localhost
hostname-strict=false

# https-port=8443

# HTTP
http-enabled=true
http-port=8080
```



## References
* Refer the official guides under the "Server" section for further reading at https://www.keycloak.org/guides
* All the keycloak configuration (`keycloak.conf` file) options can be found at https://www.keycloak.org/server/all-config 
* Official Keycloak reverse proxy guide - https://www.keycloak.org/server/reverseproxy
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MTMyNjYwNDMsMTA5MDgyNDc2MywtMT
MzNDE1MTYwLC0yNDc0NjI4NTEsMTY0NTkzMDg4MCwtODQ4NzI5
MDYzLDE0NDk2MDExMjQsLTgxMzA5NzAzNSwtMTc3ODA1NTUxMl
19
-->