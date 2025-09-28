# Keycloak behind IIS reverse proxy

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak%20iis%20architecture.png?raw=true)

- A reverse proxy like IIS can sit between clients and Keycloak server and forwards the client requests to Keycloak
- This setup can delegate common web server features like SSL, web server hardening etc. to the reverse proxy

## Install IIS on a Windows machine

- In windows search for “Turn Windows features On or Off”
- Under the “Internet Information Services” section, make sure that “IIS Management Console” and default options under “World Wide Web Services” are enabled

## IIS modules required for reverse proxy

- Install ARR and URL rewrite modules in IIS downloading them from https://www.iis.net/downloads/microsoft/application-request-routing and https://www.iis.net/downloads/microsoft/url-rewrite
- These modules enable reverse proxy features in IIS
- After installing the modules, open IIS, open “Application Request Routing”, Click on “Server Proxy Settings” in the right menu bar and make sure “Enable Proxy“ is checked.

## Website in IIS for reverse proxy

- Create a website in IIS and bind to a port (say 443)
- Use HTTPS on the website (recommended)

## URL rewrite rule

- Open the website in IIS and double click url-rewrite module
- Before creating a rule, in the right-side menu bar, click on “View Server Variables” and ensure that `HTTP_X_FORWARDED_PROTO`, `HTTP_X_FORWARDED_PORT`, `HTTP_X_FORWARDED_HOST`, `HTTP_X_FORWARDED_FOR` server variables are added
- Create a rule as shown below which to make the website act as a reverse proxy for Keycloak server which is running at http://192.168.10.11:8085
- Note that `HTTP_X_FORWARDED_PROTO`, `HTTP_X_FORWARDED_PORT`, `HTTP_X_FORWARDED_HOST`, `HTTP_X_FORWARDED_FOR` server variables are set in the url rewrite rule. This helps Keycloak to detect if a request is routed through reverse proxy. The original client request details wil be extracted in Keycloak by these headers.

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak%20iis%20url%20rewrite%20rule.png?raw=true)

## IIS web config for reverse proxy site

- Instead of graphically configuring url rewrite rule, the rule can also be added to the site’s web.config as shown below

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
        <rewrite>
            <rules>
                <rule name="keycloak" enabled="true" stopProcessing="true">
                    <match url="(.*)" />
                    <serverVariables>
                        <set name="HTTP_X_FORWARDED_PROTO" value="https" />
                        <set name="HTTP_X_FORWARDED_PORT" value="{SERVER_PORT}" />
                        <set name="HTTP_X_FORWARDED_HOST" value="{HTTP_HOST}" />
                        <set name="HTTP_X_FORWARDED_FOR" value="{REMOTE_ADDR}" />
                    </serverVariables>
                    <action type="Rewrite" url="http://192.168.10.11:8085/{R:1}" logRewrittenUrl="true" />
                    <conditions>
                    </conditions>
                </rule>
            </rules>
        </rewrite>
    </system.webServer>
</configuration>
```

## Keycloak configuration for reverse proxy

- Ensure the following settings in the `conf/keycloak.conf` file

```bash
# The proxy headers that should be accepted by the server
proxy-headers=xforwarded

# HTTP
http-enabled=true
http-port=8085

# Hostname for the Keycloak server.
# hostname=localhost
hostname-strict=false
```

## Debug reverse proxy headers and host names

- Start Keycloak with the `-hostname-debug=true` option (like `bin\kc.bat start-dev --hostname-debug=true`)
- After starting Keycloak, open the URL `https://<keycloak-host-addr>/realms/master/hostname-debug`
- This opens a page where the reverse proxy headers, hostnames received at Keycloak are displayed
- For IIS as a reverse proxy the page would show a table like

| URL | Value |
| --- | --- |
| Request | https://kubernetes.docker.internal/realms/master/hostname-debug |
| Frontend | https://kubernetes.docker.internal/ [OK] |
| Backend | https://kubernetes.docker.internal/ [OK] |
| Admin | https://kubernetes.docker.internal/ [OK] |
| Runtime | Value |
| Server mode | dev [start-dev] |
| Realm | master |
| Configuration property | Value |
| hostname-strict | false |
| hostname-strict-backchannel | false |
| hostname-strict-https | false |
| hostname-port | -1 |
| proxy | none |
| proxy-headers | xforwarded |
| http-enabled | true |
| http-relative-path | / |
| http-port | 8080 |
| https-port | 8443 |
| Header | Value |
| Host | kubernetes.docker.internal |
| X-Forwarded-For | 127.0.0.1, 127.0.0.1:51862 |
| X-Forwarded-Host | kubernetes.docker.internal |
| X-Forwarded-Port | 443 |
| X-Forwarded-Proto | https |

## Video
The video for this post can be found [here](https://youtu.be/LSJg3_uqOXU?si=mB31Wj91zia1FHhX)

<iframe width="560" height="315" src="https://www.youtube.com/embed/LSJg3_uqOXU?si=CseR3r69-LkafUyR" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## References

- Keycloak reverse proxy docs - https://www.keycloak.org/server/reverseproxy
- IIS server variables - [https://learn.microsoft.com/en-us/previous-versions/iis/6.0-sdk/ms524602(v=vs.90)](https://learn.microsoft.com/en-us/previous-versions/iis/6.0-sdk/ms524602(v=vs.90))
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ3MTY1MzAxMywxMzIxNDYxMjEzLDYwOT
YzNzk5Nyw1Nzc1MDExOV19
-->