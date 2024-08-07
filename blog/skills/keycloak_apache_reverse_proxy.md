

# Apache as reverse proxy for Keycloak 

* A reverse proxy like Apache can be used with Keycloak
* A reverse proxy sits in between the clients and server and forwards the client requests to the server

![keycloak_apache_architecture.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_apache_architecture.png?raw=true?raw=true)

## Keycloak Configuration to run behind reverse proxy

### Reverse proxy Mode - Edge
* We will use "edge" mode or SSL Termination mode of reverse proxy for this scenario.
* The requests would be in HTTPS till Apache server (reverse proxy) and Apache will send HTTP requests to Keycloak

![keycloak_edge_mode_proxy.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_edge_mode_proxy.png?raw=true)
### Other reverse proxy Modes
* In passthrough mode, HTTPS connections from clients are passed to keycloak directly without SSL termination at reverse proxy
* In reencypt mode, clients connect to reverse proxy via HTTPS and reverse proxy also connects to Keycloak via HTTPS. Hence SSL certificates are needed to be configured in reverse proxy and Keycloak.

### Request headers from reverse proxy to Keycloak
* To know the information about the client, Keycloak expects Apache (reverse proxy) to set the either the "Forwared" headers (as per [RFC7239](https://www.rfc-editor.org/rfc/rfc7239.html)) or the "X-Forwarded-*" headers.
* Apache sets "X-Forwarded-*" headers when acting as a reverse proxy. So we can configure Keycloak accordingly.

### Settings in keycloak.conf file
* The following settings can be used in the `keycloak.conf` file for running behind an Apache reverse proxy
* `http-enabled=true` and `http-port=8080` is used since Apache communicated to Keycloak over HTTP
* `proxy-headers=xforwarded` is used since Apache sets the "X-Forwarded-*" headers (In older versions of keycloak, `proxy=edge` can be used).
* Certificate file paths are configured for running keycloak in production mode
* Hostname is configured as dynamic using  `hostname-strict=false` (Single hostname like `hostname=localhost` can also be used).

```apacheconf
## keycloak.conf file

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

## Apache configuration to run as a reverse proxy
* Enable mod_proxy, mod_proxy_http, mod_ssl, mod_headers, mod_socache_shmcb modules in the httpd.conf file
* Add a line `Include conf/extra/kc_reverse_proxy.conf` in the httpd.conf file of the Apache server
* Create a file named `kc_reverse_proxy.conf` in the conf/extra folder of Apache server as shown below

```apacheconf
## conf/extra/kc_reverse_proxy.conf file

Listen 443

#   SSL Cipher Suite:
SSLCipherSuite HIGH:MEDIUM:!MD5:!RC4:!3DES
SSLProxyCipherSuite HIGH:MEDIUM:!MD5:!RC4:!3DES

#   SSL Protocol support:
SSLProtocol all -SSLv3 -TLSv1
SSLProxyProtocol all -SSLv3 -TLSv1

#   Pass Phrase Dialog:
SSLPassPhraseDialog  builtin

#   Inter-Process Session Cache:
#SSLSessionCache         "dbm:${SRVROOT}/logs/ssl_scache"
SSLSessionCache        "shmcb:${SRVROOT}/logs/ssl_scache(512000)"
SSLSessionCacheTimeout  300

<VirtualHost _default_:443>
    ServerName catchall
    ServerAdmin admin@example.com

    ErrorLog "${SRVROOT}/logs/error.log"
    TransferLog "${SRVROOT}/logs/access.log"
    
    SSLEngine on
    SSLCertificateFile "${SRVROOT}/conf/server.crt"
    SSLCertificateKeyFile "${SRVROOT}/conf/server.key"

    ProxyRequests Off
    ProxyPreserveHost On
    ProxyAddHeaders On
    
    SSLProxyEngine On
    SSLProxyCheckPeerCN on
    SSLProxyCheckPeerExpire on

    RequestHeader set X-Forwarded-Proto https
    RequestHeader set X-Forwarded-Port 443

    ProxyPass / http://127.0.0.1:8080/
    ProxyPassReverse / http://127.0.0.1:8080/
</VirtualHost>
```
* Using the above configuration, a virtual host is created that listens on port 443 over HTTPS.
* All the requests are being passes to the Keycloak server running at `http://127.0.0.1:8080/`.
*  `RequestHeader set X-Forwarded-Proto https` and `RequestHeader set X-Forwarded-Port 443` are configured to pass the client request protocol and port information to Keycloak server.
* `ProxyAddHeaders On` will add additional headers (X-Forwarded-For, X-Forwarded-Host and X-Forwarded-Server) to the request and pass them to Keycloak server.
* `ProxyPreserveHost On` will set the same hostname as the client request header in the proxied request `Host` header.
* `SSLProxyEngine on` is used to enable HTTPS in reverse proxy.
* `SSLProxyCheckPeerCN on` means Apache will check if request URL hostname and server certificate CN (common name) are the same. If both are not same, 502 (bad gateway) response will be given.
* `SSLProxyCheckPeerExpire on` means Apache will check if the server certificate is expired. If expired, 502 (Bad gateway).

### Exposing only selected paths via Apache (reverse proxy)
* Admin console can be hidden from clients via reverse proxy to avoid security risks. If required, admin panel can be accessed via localhost or internal LAN.
* The following Apache (reverse proxy) configuration can be used to expose only required paths to clients and expose all paths only on localhost

```apacheconf
Listen 443

#   SSL Cipher Suite:
SSLCipherSuite HIGH:MEDIUM:!MD5:!RC4:!3DES
SSLProxyCipherSuite HIGH:MEDIUM:!MD5:!RC4:!3DES

#   SSL Protocol support:
SSLProtocol all -SSLv3 -TLSv1
SSLProxyProtocol all -SSLv3 -TLSv1

#   Pass Phrase Dialog:
SSLPassPhraseDialog  builtin

#   Inter-Process Session Cache:
#SSLSessionCache         "dbm:${SRVROOT}/logs/ssl_scache"
SSLSessionCache        "shmcb:${SRVROOT}/logs/ssl_scache(512000)"
SSLSessionCacheTimeout  300

<VirtualHost localhost:443>
    ServerName localhost
    ServerAdmin admin@example.com

    ErrorLog "${SRVROOT}/logs/error.log"
    TransferLog "${SRVROOT}/logs/access.log"
    
    SSLEngine on
    SSLCertificateFile "${SRVROOT}/conf/server.crt"
    SSLCertificateKeyFile "${SRVROOT}/conf/server.key"

    ProxyRequests Off
    ProxyPreserveHost On
    ProxyAddHeaders On
    
    SSLProxyEngine On
    SSLProxyCheckPeerCN On
    SSLProxyCheckPeerExpire On

    RequestHeader set X-Forwarded-Proto https
    RequestHeader set X-Forwarded-Port 443

    ProxyPass / http://127.0.0.1:8080/
    ProxyPassReverse / http://127.0.0.1:8080/
</VirtualHost>

<VirtualHost _default_:443>
    ServerName catchall
    ServerAdmin admin@example.com

    ErrorLog "${SRVROOT}/logs/error.log"
    TransferLog "${SRVROOT}/logs/access.log"
    
    SSLEngine on
    SSLCertificateFile "${SRVROOT}/conf/server.crt"
    SSLCertificateKeyFile "${SRVROOT}/conf/server.key"

    ProxyRequests Off
    ProxyPreserveHost On
    ProxyAddHeaders On
    
    SSLProxyEngine On
    SSLProxyCheckPeerCN On
    SSLProxyCheckPeerExpire On

    RequestHeader set X-Forwarded-Proto https
    RequestHeader set X-Forwarded-Port 443

    ProxyPass /js/ http://127.0.0.1:8080/js/
    ProxyPassReverse /js/ http://127.0.0.1:8080/js/

    ProxyPass /realms/ http://127.0.0.1:8080/realms/
    ProxyPassReverse /realms/ http://127.0.0.1:8080/realms/

    ProxyPass /resources/ http://127.0.0.1:8080/resources/
    ProxyPassReverse /resources/ http://127.0.0.1:8080/resources/

    ProxyPass /robots.txt http://127.0.0.1:8080/robots.txt
    ProxyPassReverse /robots.txt http://127.0.0.1:8080/robots.txt
</VirtualHost>
```
* As shown above, two virtual hosts are created in Apache. 
* One virtual host exposes all paths of keycloak but listens only on localhost.
* Another virtual host exposes only recommended paths. This can be accessed by clients.

### Video
You can see the video for this post [here](https://youtu.be/YCQJtj0YvR8?si=8ff3_r0qD1R25m3q)

<iframe width="560" height="315" src="https://www.youtube.com/embed/YCQJtj0YvR8?si=i7fssgtgMkGUSNki" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


## References
* Official Keycloak reverse proxy guide - https://www.keycloak.org/server/reverseproxy
* Refer the official guides under the "Server" section for further reading at https://www.keycloak.org/guides
* All the keycloak configuration (`keycloak.conf` file) options can be found at https://www.keycloak.org/server/all-config 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NjAyNjQzNzAsLTQwNjIwNTA3MCw4Mj
A1OTA5MzAsMTUzMjIwNzI3NCwtNDQyNjYxMzA0LC01MTI3NDE1
OTIsMTg2NTY3NjYxMyw1NjQ5NTQ0NDEsLTQ2NDU5NDYxOSwxMD
kwODI0NzYzLC0xMzM0MTUxNjAsLTI0NzQ2Mjg1MSwxNjQ1OTMw
ODgwLC04NDg3MjkwNjMsMTQ0OTYwMTEyNCwtODEzMDk3MDM1LC
0xNzc4MDU1NTEyXX0=
-->