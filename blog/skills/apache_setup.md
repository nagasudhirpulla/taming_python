## Setup Apache web server in windows using Apache Lounge

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

## Why use Apache web server

Some of the use cases for using Apache web server is

-   Static file hosting
-   Reverse proxy
-   Hosting servers than render PHP, Perl, Lua scripts
-   FTP
-   URL rewriting
-   Gzip compression and decompression

and many more

## Setup Apache server for windows

-   Apache for windows is not available from Apache foundation but available from third party vendors like Apache lounge
-   Download the zip from Apache lounge and extract the “Apache24” folder into C folder
-   Register Apache server as a windows service using the command inside the bin folder

```powershell
httpd.exe -k install

```

-   Check Apache configuration using the command inside bin folder

```powershell
httpd.exe -t

```

-   Now a web page should be displayed in the browser at [http://locahost](http://locahost)
-   The static content is served from htdocs folder

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a8438548-059b-46f7-ae8b-dbf497d7bb77/Untitled.png)

## Configure server with httpd.conf file

-   httpd.conf file can be used to configure the web server. It is present in the conf folder
-   Various modules can be enabled and disabled from this file
-   Other configuration files can be included in this file
-   Many configuration files covering different scenarios like reverse proxy, ssl etc are present in the conf/extra folder for reference. We can create our own configuration file by using these reference configuration files
-   [Apache Conf](https://marketplace.visualstudio.com/items?itemName=mrmlnc.vscode-apache) VS code extension can be used for easy syntax highlighting of the config files
-   Out of the box, the httpd.conf of the server is configured to listen on port 80 and server static content from the htdocs folder. Also a lot of best practices are implemented in the httpd.conf file

## Serve static files using directory browsing

-   The following configuration in the httpd.conf file configures the web server to serve static content from htdocs folder

```bash
# DocumentRoot: The directory out of which you will serve your
# documents. By default, all requests are taken from this directory, but
# symbolic links and aliases may be used to point to other locations.
#
DocumentRoot "${SRVROOT}/htdocs"
<Directory "${SRVROOT}/htdocs">
    #
    # Possible values for the Options directive are "None", "All",
    # or any combination of:
    #   Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews
    #
    # Note that "MultiViews" must be named *explicitly* --- "Options All"
    # doesn't give it to you.
    #
    # The Options directive is both complicated and important.  Please see
    # <http://httpd.apache.org/docs/2.4/mod/core.html#options>
    # for more information.
    #
    Options Indexes FollowSymLinks

    #
    # AllowOverride controls what directives may be placed in .htaccess files.
    # It can be "All", "None", or any combination of the keywords:
    #   AllowOverride FileInfo AuthConfig Limit
    #
    AllowOverride None

    #
    # Controls who can get stuff from this server.
    #
    Require all granted
</Directory>

#
# DirectoryIndex: sets the file that Apache will serve if a directory
# is requested.
#
<IfModule dir_module>
    DirectoryIndex index.html
</IfModule>

```

-   _Options Indexes FollowSymLinks_ means the options Indexes and FollowSymLinks are enabled. _Indexes_ means, if no index page is present in a folder, the folder contents will be shown to the user. _FollowSymlinks_ means that the server will follow a symbolic link (or a file shortcut) if present. Do not use FollowSymLinks if not required
-   _AllowOverride None_ means, the configuration of the directive is not allowed to be changed by the .htaccess files
-   _Require all granted_ means, all can access the folder contents with out any authorization
-   _DirectoryIndex index.html_ means, if a directory is requested, this index.html will be served if present

## Multiple web servers using virtual hosts

-   Virtual hosts are a way to run multiple servers each with different server name or listening port in a single Apache server
-   For example, the below configuration can host two directories each listening for different hostnames on port 80

```xml
<VirtualHost *:80>
    ServerAdmin webmaster@dummy-host.example.com
    DocumentRoot "${SRVROOT}/docs/dummy1"
    ServerName dummy-host.example.com
    ServerAlias www.dummy-host.example.com
    ErrorLog "logs/dummy-host.example.com-error.log"
</VirtualHost>

<VirtualHost *:80>
    ServerAdmin webmaster@dummy-host2.example.com
    DocumentRoot "${SRVROOT}/docs/dummy2"
    ServerName dummy-host2.example.com
    ErrorLog "logs/dummy-host2.example.com-error.log"
</VirtualHost>

```

-   In the above example configuration, the two virtual hosts are listening on the same port 80, but if the hostname in the request is “[dummy-host.example.com](http://dummy-host.example.com)” the request will be handled by the first virtual host and if the hostname in the request is “[dummy-host2.example.com](http://dummy-host2.example.com)”, the request will be handled by the second virtual host
-   The first virtual host serves the folder “/docs/dummy1”
-   The second virtual host serves the folder “/docs/dummy2”
-   Different ports can also be linked to multiple virtual hosts based on the requirement

## Enable modules in Apache server using httpd.conf file

-   Just un-comment the relevant line in httpd.conf file to enable modules in Apache server. Remove “#” at the start of the line to un-comment it.
-   For example, to enable the module “mod_proxy” in Apache server, un-comment the line “LoadModule proxy_module modules/mod_proxy.so” in the httpd.conf file

## Using SSL for running over HTTPS

### Create localhost SSL certificate for testing purposes

-   Run the following command in the Apache folder and provide the required inputs. This command uses OpenSSL to create SSL certificate and SSL private key

```bash
.\\bin\\openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 -keyout "conf/server.key" -out "conf/server.crt"

```

-   The generated SSL certificate and SSL private key files can be used for HTTPS hosting on localhost

### Modules to be enabled

-   Enable the mod_ssl, mod_headers, mod_socache_shmcb modules in the httpd.conf file

### Configuration for HTTPS in a virtual host

```bash
# test_ssl.conf
Listen 443

#   SSL Cipher Suite:
#   List the ciphers that the client is permitted to negotiate,
#   and that httpd will negotiate as the client of a proxied server.
#   See the OpenSSL documentation for a complete list of ciphers, and
#   ensure these follow appropriate best practices for this deployment.
#   httpd 2.2.30, 2.4.13 and later force-disable aNULL, eNULL and EXP ciphers,
#   while OpenSSL disabled these by default in 0.9.8zf/1.0.0r/1.0.1m/1.0.2a.
SSLCipherSuite HIGH:MEDIUM:!MD5:!RC4:!3DES
SSLProxyCipherSuite HIGH:MEDIUM:!MD5:!RC4:!3DES

#   SSL Protocol support:
#   List the protocol versions which clients are allowed to connect with.
#   Disable SSLv3 by default (cf. RFC 7525 3.1.1).  TLSv1 (1.0) should be
#   disabled as quickly as practical.  By the end of 2016, only the TLSv1.2
#   protocol or later should remain in use.
SSLProtocol all -SSLv3 -TLSv1
SSLProxyProtocol all -SSLv3 -TLSv1

#   Pass Phrase Dialog:
#   Configure the pass phrase gathering process.
#   The filtering dialog program (`builtin' is an internal
#   terminal dialog) has to provide the pass phrase on stdout.
SSLPassPhraseDialog  builtin

#   Inter-Process Session Cache:
#   Configure the SSL Session Cache: First the mechanism 
#   to use and second the expiring timeout (in seconds).
#SSLSessionCache         "dbm:${SRVROOT}/logs/ssl_scache"
SSLSessionCache        "shmcb:${SRVROOT}/logs/ssl_scache(512000)"
SSLSessionCacheTimeout  300

<Directory "C:\\Users\\James\\Pictures">
    AllowOverride None
    Require all granted
</Directory>

<VirtualHost _default_:443>
    ServerName localhost:443
    ServerAdmin admin@example.com

    ErrorLog "${SRVROOT}/logs/error.log"
    TransferLog "${SRVROOT}/logs/access.log"
    
    SSLEngine on
    SSLCertificateFile "${SRVROOT}/conf/server.crt"
    SSLCertificateKeyFile "${SRVROOT}/conf/server.key"

    ProxyRequests Off

    DocumentRoot "C:\\Users\\James\\Pictures"
    Options Indexes
</VirtualHost>

```

-   The above example configuration is used to setup a virtual host to listen on port 443 over HTTPS and server a local directory.
-   A file “conf/extra/test_ssl.conf” is created with the above configuration in it. Make sure to include this configuration in the httpd.conf file by adding the line “Include conf/extra/test_ssl.conf” in the file
-   The configuration is as follows
    -   Since we require to listen in 443, we need to explicitly mention “Listen 443", since only port 80 is used by default by Apache server
    -   The next configuration is to set the Cipher suites for HTTPS negotiation between client and server
    -   The next configuration is to configure the supported SSL protocols
    -   The next configurations are for configuring SSL passphrase and session cache timeout
    -   In this example, we are serving a folder “C:\Users\James\Pictures”. But the folder access needs to be explicitly given to the Apache server. We have granted permission to access the folder using the “<Directory "C:\Users\James\Pictures">” section.
    -   In the virtual host section we have configured the log files location, SSL certificates and directory hosting location, enabled directory listing of the folder.

## Configure reverse proxy

### Modules to be enabled

-   Enable the modules mod_proxy, mod_proxy_http, mod_ssl, mod_headers, mod_socache_shmcb in the httpd.conf file

```bash
# test_reverse_proxy.conf
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
    ServerName localhost:443
    ServerAdmin admin@example.com

    ErrorLog "${SRVROOT}/logs/error.log"
    TransferLog "${SRVROOT}/logs/access.log"
    
    SSLEngine on
    SSLCertificateFile "${SRVROOT}/conf/server.crt"
    SSLCertificateKeyFile "${SRVROOT}/conf/server.key"

    ProxyRequests Off
    ProxyPreserveHost On
    
    SSLProxyEngine On
    SSLProxyCheckPeerCN on
    SSLProxyCheckPeerExpire on

    RequestHeader set X-Forwarded-Proto "https"
    RequestHeader set X-Forwarded-Port "443"
    ProxyPass /test <http://127.0.0.1:8080/>
    ProxyPassReverse /test <http://127.0.0.1:8080/>
</VirtualHost>

```

-   A file named “test_reverse_proxy.conf” can be created and included in the httpd.conf by adding the line “Include conf/extra/test_reverse_proxy.conf” in the file
-   The above configuration makes the Apache web server to listen on HTTPS and act as a reverse proxy for an application running at “[http://127.0.0.1:8080/”](http://127.0.0.1:8080/%E2%80%9D) when the request path starts with “/path”
-   Enable mod_proxy, mod_proxy_http, mod_ssl, mod_headers, mod_socache_shmcb modules in the httpd.conf file
-   **ProxyAddHeaders on** passes _X-Forwarded-Host_, _XForwarded-For_, and _X-Forwarded-Server_ headers to the back-end server by default
-   **ProxyPreserveHost on** retains the original host from the client browser
-   **SSLProxyEngine on** is used to enable SSL in reverse proxy
-   **SSLProxyCheckPeerCN on** means Apache will check if request URL hostname and server certificate CN (common name) are the same. If both are not same, 502 (bad gateway) response will be given
-   **SSLProxyCheckPeerExpire on** means Apache will check if the server certificate is expired. If expired, 502 (Bad gateway) response will be given

## References

-   Tutorial to setup reverse proxy in Apache config - [](http://www.apachetutor.org/admin/reverseproxies)[http://www.apachetutor.org/admin/reverseproxies](http://www.apachetutor.org/admin/reverseproxies)
-   virtual host explained - [](https://dasunhegoda.com/what-how-to-apache-virtual-host/444/)[https://dasunhegoda.com/what-how-to-apache-virtual-host/444/](https://dasunhegoda.com/what-how-to-apache-virtual-host/444/)
-   ProxyPreserveHost - [](https://docs.oracle.com/cd/E93962_01/bigData.Doc/install_onPrem/src/cins_studio_reverse_proxy_apache_proxypreservehost.html)[https://docs.oracle.com/cd/E93962_01/bigData.Doc/install_onPrem/src/cins_studio_reverse_proxy_apache_proxypreservehost.html](https://docs.oracle.com/cd/E93962_01/bigData.Doc/install_onPrem/src/cins_studio_reverse_proxy_apache_proxypreservehost.html)
-   SSLProxyEngine on - [](https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine)[https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine](https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine)
-   SSLProxyCheckPeerCN on - [](https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxycheckpeercn)[https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxycheckpeercn](https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxycheckpeercn)
-   SSLProxyCheckPeerExpire on - [](https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxycheckpeerexpire)[https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxycheckpeerexpire](https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxycheckpeerexpire)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MjgxNzg4NzBdfQ==
-->