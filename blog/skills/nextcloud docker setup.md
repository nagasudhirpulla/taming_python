# Nextcloud docker-compose setup

## What is Nextcloud

**Nextcloud** is an open-source software suite for secure file storage and team collaboration.

- **Self-Hosted alternative:** Replaces services like Google Drive.
- **Complete Control:** On-premises or in the cloud deployment to maintain full data ownership.

## Features

Features deployed in this Nextcloud docker-compose based deployment are:

- Files hosting - like google drive
- Web based collaborative document editing of word, spreadsheet, PowerPoint files - like google docs, sheets, slides
- Text, Audio, Video messaging and conference - like google meet or whatsapp

## Architecture

![architecture.svg](https://raw.githubusercontent.com/nagasudhirpulla/taming_python/8f7a3c90d63d696b04d13a09e6d53b405ebdc0cb/blog/skills/assets/img/nextcloud%20docker%20architecture.svg)

- nextcloud container hosts the main nextcloud application
- Nextcloud container uses PostgreSQL container as database and Redis container for caching.
- collabora/code container hosts the collaborative document editing server
- aio-talk container hosts the high performance backend for nextcloud talk
- Apache reverse proxy container exposes nextcloud, collaboara/code, aio-talk container to the clients. Nextcloud container also accesses the collabora/code and aio-talk containers using the reverse proxy.

## Docker Containers

This setup uses the following containers declared in a docker compose file

- Nextcloud app:
    - nextcloud:apache - main Nextcloud application
    - postgres:alpine - PostgreSQL database for Nextcloud
    - redis:alpine - Redis caching for Nextcloud
- Backends for Nextcloud plugins:
    - collabora/code - collaborative document editing backend for Nextcloud
    - aio-talk - nextcloud talk backend application
- httpd - Apache reverse proxy to expose nextcloud, collabora, nextcloud-talk applications
- paulczar/omgwtfssl - Self-signed certificates generation for local domains of nextcloud, collabora, nextcloud talk applications

## Configure Nextcloud container

### Apps in Nextcloud

- Apps extend the functionality of a Nextcloud installation (like plugins)
- The following additional apps are installed our nextcloud installation
    - richdocuments - enables nextcloud office collaborative document editing features (word, spreadsheets, slides)
    - spreed - enables nextcloud talk for audio/video conferencing and chats

### Install and configure Nextcloud apps with occ commands

- Nextcloud occ (OwnCloud Console) is the built-in command-line interface to manage and administer the Nextcloud installation
- The following occ commands are run in the nextcloud server to install and configure apps and features to use external real-time document editing and audio/video messaging containers

```bash
# # set default app to dashboard
# php occ config:system:set defaultapp --value=dashboard

# rely on system cron to update nextcloud periodically
php occ background:cron

# install nextcloud office app
php occ app:install richdocuments

# install nextcloud talk app
php occ app:install spreed

# install nextcloud drawio app
php occ app:install drawio

# # install nextcloud built in code server instead of a separate collabora online server
# php -d memory_limit=512M occ app:install richdocumentscode

# occ commands for collabora/code server configurations in nextcloud - https://github.com/nextcloud/richdocuments/blob/main/docs/install.md#configure-the-app-from-the-commandline

# set collabora online server URL
php occ config:app:set richdocuments wopi_url --value="https://$COLLABORA_FQDN"

# Disable SSL certificate verification (use only for testing!)
[ "$SKIP_CERT_VERIFY" = "true" ] && export disable_cert_verification="yes" || export disable_cert_verification="no"
php occ config:app:set richdocuments disable_certificate_verification --value="$disable_cert_verification"

# occ commands for nextcloud talk server configuration in nextcloud - https://nextcloud-talk.readthedocs.io/en/latest/occ/#talksignalingadd
# add high performance backend (signaling server) for nextcloud talk
php occ talk:signaling:add "https://${SIGNAL_FQDN}" "${SIGNALING_SECRET}"

# add stun server for nextcloud talk
php occ talk:stun:add "${SIGNAL_FQDN}:3478"
# remove default stun server
php occ talk:stun:delete "stun.nextcloud.com:443"

# configure turn server for nextcloud talk
php occ talk:turn:add "turn" "${SIGNAL_FQDN}:3478" "udp,tcp" --secret="${TURN_SECRET}"

```

### Setup Nextcloud to run behind Reverse Proxy with SSL termination

- An apache reverse proxy is used to expose nextcloud, collabora/code and aio-talk conatainers to the clients instead of directly exposing the containers.
- The reverse proxy also handles SSL termination, so SSL certificates need not be configured in the application containers.
- The following occ commands are run in the nextcloud server to declare that a reverse proxy is running to expose nextcloud application with SSL termination. Please note that the reverse proxy’s network IP address is dynamically derived using its docker container name

```bash
# 1. Enforce HTTPS for all generated Nextcloud absolute URLs
php occ config:system:set overwriteprotocol --value="https"

# 2. Dynamically fetch the "proxy" container IP and append it safely to trusted_proxies
proxy_ip=$(getent hosts proxy | awk '{print $1}')
php occ config:system:set trusted_proxies 0 --value="$proxy_ip"
php occ config:system:set trusted_proxies 1 --value="127.0.0.1"
php occ config:system:set trusted_proxies 2 --value="app"

# 3. Lock down the public-facing domain name
php occ config:system:set overwritehost --value="$NEXTCLOUD_FQDN"

# 4. Ensure background cron jobs generate correct URLs in emails/notifications
php occ config:system:set overwrite.cli.url --value="https://$NEXTCLOUD_FQDN"

# # config.php location in nextcloud container is /var/www/html/config/config.php. Check here if the values are set correctly 
```

### Run shell scripts just after installation in Nextcloud

- Nextcloud runs any scripts present in the `/docker-entrypoint-hooks.d/post-installation` folder of the container. Hence the folder containing required occ commands to install and configure required applications is mounted at the container’s `/docker-entrypoint-hooks.d/post-installation` folder location
- If the post-installation scripts could not run correctly due to some reason, they can be run again using the following scripts

```
docker exec -u www-data -i app sh < .\nextcloud\appHooks\post-installation\00_indicate_rev_proxy_https.sh
docker exec -u www-data -i app sh < .\nextcloud\appHooks\post-installation\01_install_apps.sh
```

To run scripts from Linux based workstations, use the following commands instead

```bash
docker exec -u www-data -i app sh < ./nextcloud/appHooks/post-installation/00_indicate_rev_proxy_https.sh
docker exec -u www-data -i app sh < ./nextcloud/appHooks/post-installation/01_install_apps.sh
```

## Reverse proxy container setup

### Reverse proxy virtual host for nextcloud

```bash
# nextcloud reverse proxy apache configuration
Listen 443

#   SSL Cipher Suite:
SSLCipherSuite ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384
SSLProxyCipherSuite HIGH:MEDIUM:!MD5:!RC4:!3DES

#   SSL Protocol support:
SSLProtocol             all -SSLv3 -TLSv1 -TLSv1.1
SSLHonorCipherOrder     off
SSLSessionTickets       off

# enable ssl stapling if you are using a valid certificate from a trusted CA and have OCSP support enabled on the CA side
SSLUseStapling          Off
# SSLStaplingCache "shmcb:logs/ssl_stapling(32768)"

#   Pass Phrase Dialog:
SSLPassPhraseDialog  builtin

#   Inter-Process Session Cache:
#SSLSessionCache         "dbm:${SRVROOT}/logs/ssl_scache"
SSLSessionCache        "shmcb:logs/ssl_scache(512000)"
SSLSessionCacheTimeout  300

# Prevent timeout limits on heavy processing paths like /login
ProxyTimeout 300
KeepAlive On
MaxKeepAliveRequests 100
KeepAliveTimeout 5

<VirtualHost _default_:443>
    ServerName ${NEXTCLOUD_FQDN}
    # ServerAdmin admin@example.com

    # Logging
    ErrorLog "logs/nextcloud-error.log"
    CustomLog "logs/nextcloud-access.log" combined
    
    # SSL Configuration
    SSLEngine on
    SSLCertificateFile "conf/certs/${NEXTCLOUD_FQDN}.crt"
    SSLCertificateKeyFile "conf/certs/${NEXTCLOUD_FQDN}.key"

    # Security Headers
    Header always set Strict-Transport-Security "max-age=15552000; includeSubDomains"
    Header always set X-Content-Type-Options "nosniff"

    # Nextcloud Discovery Redirects

    # <IfModule mod_rewrite.c>
    #     RewriteEngine on
    #     RewriteRule ^/.well-known/carddav https://%{SERVER_NAME}/remote.php/dav [R=301,L]
    #     RewriteRule ^/.well-known/caldav https://%{SERVER_NAME}/remote.php/dav [R=301,L]
    # </IfModule>
    
    Redirect 301 /.well-known/carddav /remote.php/dav
    Redirect 301 /.well-known/caldav /remote.php/dav
    Redirect 301 /.well-known/webfinger /index.php/.well-known/webfinger
    Redirect 301 /.well-known/nodeinfo /index.php/.well-known/nodeinfo

    # Proxy Core Settings
    ProxyRequests Off
    ProxyPreserveHost On
    ProxyAddHeaders On

    # Real IP Forwarding Headers
    RequestHeader set X-Forwarded-Proto "https"
    RequestHeader set X-Forwarded-Port "443"

     # WebSocket Support Mapping (Required for Real-time Push and Nextcloud Talk)
    ProxyPassMatch ^/(.*)/ws$ ws://app/$1/ws

    # Main Reverse Proxy Pass
    # ProxyPassReverse intercepts and rewrites the "Location" header during redirects
    ProxyPass / http://app/
    ProxyPassReverse / http://app/

    # SSLProxyEngine On
    # SSLProxyCheckPeerCN on
    # SSLProxyCheckPeerExpire on

    SSLProxyVerify none
    SSLProxyCheckPeerCN off
    SSLProxyCheckPeerName off
</VirtualHost>

# see the logs in container at /usr/local/apache2/logs/ folder
```

### Reverse proxy virtual host for collabora/code

```bash
########################################
# Reverse proxy for Collabora Online
########################################

<VirtualHost _default_:443>
    AllowEncodedSlashes NoDecode

    ServerName ${COLLABORA_FQDN}:443
    # ServerAdmin admin@example.com

    # Logging
    ErrorLog "logs/errorCollabora.log"
    TransferLog "logs/accessCollabora.log"

    # SSL configuration
    SSLProxyEngine On
    SSLCertificateFile "conf/certs/${COLLABORA_FQDN}.crt"
    SSLCertificateKeyFile "conf/certs/${COLLABORA_FQDN}.key"

    # Security Headers
    Header always set Strict-Transport-Security "max-age=15552000; includeSubDomains"
    Header always set X-Content-Type-Options "nosniff"

    # Proxy core settings
    ProxyPreserveHost On
    ProxyRequests Off
    ProxyAddHeaders On

    # static html, js, images, etc. served from coolwsd
    # browser is the client part of Collabora Online
    ProxyPass           /browser http://collabora:9980/browser retry=0
    ProxyPassReverse    /browser http://collabora:9980/browser

    # WOPI discovery URL
    ProxyPass           /hosting/discovery http://collabora:9980/hosting/discovery retry=0
    ProxyPassReverse    /hosting/discovery http://collabora:9980/hosting/discovery

    # Capabilities
    ProxyPass           /hosting/capabilities http://collabora:9980/hosting/capabilities retry=0
    ProxyPassReverse    /hosting/capabilities http://collabora:9980/hosting/capabilities

    # Main websocket
    ProxyPassMatch      "/cool/(.*)/ws$"      ws://collabora:9980/cool/$1/ws nocanon

    # Admin Console websocket
    ProxyPass           /cool/adminws ws://collabora:9980/cool/adminws

    # Download as, Fullscreen presentation and Image upload operations
    ProxyPass           /cool http://collabora:9980/cool
    ProxyPassReverse    /cool http://collabora:9980/cool
    # Compatibility with integrations that use the /lool/convert-to endpoint
    ProxyPass           /lool http://collabora:9980/cool
    ProxyPassReverse    /lool http://collabora:9980/cool

    SSLProxyVerify None
    SSLProxyCheckPeerCN Off
    SSLProxyCheckPeerName Off
</VirtualHost>
```

### Reverse proxy virtual host for aio-talk

```bash
<VirtualHost _default_:443>
    AllowEncodedSlashes NoDecode
    SSLProxyEngine On
    ProxyPreserveHost On

    ServerName ${SIGNAL_FQDN}:443
    # ServerAdmin admin@example.com

    # Logging
    ErrorLog "logs/talk-error.log"
    TransferLog "logs/talk-access.log"
    
    # SSL Configuration
    SSLEngine on
    SSLCertificateFile "conf/certs/${SIGNAL_FQDN}.crt"
    SSLCertificateKeyFile "conf/certs/${SIGNAL_FQDN}.key"

    # Security Headers
    Header always set Strict-Transport-Security "max-age=15552000; includeSubDomains"
    Header always set X-Content-Type-Options "nosniff"

    # Proxy Core Settings
    ProxyRequests Off
    ProxyPreserveHost On
    ProxyAddHeaders On
    RewriteEngine On

    # Real IP Forwarding Headers
    RequestHeader set X-Forwarded-Proto expr=%{REQUEST_SCHEME}
    RequestHeader set X-Real-IP expr=%{REMOTE_ADDR}
    ProxyPass / http://talk_hpb:8081/ upgrade=websocket

    # SSLProxyEngine On
    # SSLProxyCheckPeerCN on
    # SSLProxyCheckPeerExpire on
    
    SSLProxyVerify None
    SSLProxyCheckPeerCN Off
    SSLProxyCheckPeerName Off
</VirtualHost>
```

### Nextcloud proxy apache dockerfile

- The reverse proxy container exposes nextcloud, collabora and nextcloud talk container services to the internet
- The docker file below adds required files (virtual host config files) and modifications to httpd image (enabling required modules)

```docker
FROM httpd:alpine
COPY --chmod=664 nextcloud.conf /usr/local/apache2/conf/nextcloud.conf
COPY --chmod=664 collabora.conf /usr/local/apache2/conf/collabora.conf
COPY --chmod=664 signal.conf /usr/local/apache2/conf/signal.conf
COPY --chmod=664 self_signed/true.conf /usr/local/apache2/conf/extra/self_signed/true.conf
COPY --chmod=664 self_signed/false.conf /usr/local/apache2/conf/extra/self_signed/false.conf
RUN set -ex; \
    sed -i \
            -e '/^Listen /d' \
            -e 's/^#\(LoadModule .*mod_proxy.so\)/\1/' \
            -e 's/^#\(LoadModule .*mod_proxy_http.so\)/\1/' \
            -e 's/^#\(LoadModule .*mod_ssl.so\)/\1/' \
            -e 's/^#\(LoadModule .*mod_headers.so\)/\1/' \
            -e 's/^#\(LoadModule .*mod_rewrite.so\)/\1/' \
            -e 's/^#\(LoadModule .*mod_proxy_wstunnel.so\)/\1/' \
            -e 's/^#\(LoadModule .*mod_socache_shmcb.so\)/\1/' \
        /usr/local/apache2/conf/httpd.conf; \
    echo "Include conf/nextcloud.conf" | tee -a /usr/local/apache2/conf/httpd.conf; \
    echo "Include conf/collabora.conf" | tee -a /usr/local/apache2/conf/httpd.conf; \
    echo "Include conf/signal.conf" | tee -a /usr/local/apache2/conf/httpd.conf;
```

## Nextcloud Docker compose setup with required containers

```docker
services:
  # Postgres DB for nextcloud. Reference: https://hub.docker.com/_/postgres
  db:
    # Note: Check the recommend version here: https://docs.nextcloud.com/server/latest/admin_manual/installation/system_requirements.html#server
    image: postgres:alpine
    container_name: db
    restart: always
    volumes:
      - db:/var/lib/postgresql:Z
    env_file:
      - db.env

  # Redis for nextcloud. Reference - https://hub.docker.com/_/redis
  redis:
    image: redis:alpine
    container_name: redis
    restart: always

  # main nextcloud app container. Reference - https://hub.docker.com/_/nextcloud
  app:
    image: nextcloud:apache
    container_name: app
    hostname: app
    restart: always
    ports:
      - 8080:80
    volumes:
      # NOTE: The `volumes` config of the `cron` and `app` containers must match
      - nextcloud:/var/www/html:z
      - ./nextcloud/appHooks/post-installation:/docker-entrypoint-hooks.d/post-installation
    # - /nas:/nas
    # - ./nextcloud/appHooks/before-starting:/docker-entrypoint-hooks.d/before-starting
    environment:
      POSTGRES_HOST: db
      REDIS_HOST: redis
      NEXTCLOUD_TRUSTED_DOMAINS: "${NEXTCLOUD_FQDN} app 127.0.0.1"
      NEXTCLOUD_ADMIN_USER: ${NEXTCLOUD_UNAME}
      NEXTCLOUD_ADMIN_PASSWORD: ${NEXTCLOUD_PWD}
      NEXTCLOUD_FQDN: ${NEXTCLOUD_FQDN}
      COLLABORA_FQDN: ${COLLABORA_FQDN}
      SIGNAL_FQDN: ${SIGNAL_FQDN}
      SIGNALING_SECRET: ${SIGNALING_SECRET}
      SKIP_CERT_VERIFY: ${SKIP_CERT_VERIFY} # true for local self-signed certs; false for CA-issued valid SSL certificates
      TURN_SECRET: ${TURN_SECRET}
    env_file:
      - db.env
    depends_on:
      - db
      - redis
      - proxy
    networks:
      - default
      - proxy-tier

  # Apache reverse-proxy to expose nextcloud to the clients. Reference: https://hub.docker.com/_/httpd
  proxy:
    build: ./proxy
    restart: always
    container_name: proxy
    hostname: proxy
    ports:
      - 443:443
    volumes:
      - ./certs:/usr/local/apache2/conf/certs:ro,z
    networks:
      proxy-tier:
        aliases:
          - ${NEXTCLOUD_FQDN}
          - ${COLLABORA_FQDN}
          - ${SIGNAL_FQDN}
    environment:
      NEXTCLOUD_FQDN: ${NEXTCLOUD_FQDN}
      COLLABORA_FQDN: ${COLLABORA_FQDN}
      SIGNAL_FQDN: ${SIGNAL_FQDN}
      # keep this false when moving to CA-issued valid SSL certificates
      SKIP_CERT_VERIFY: ${SKIP_CERT_VERIFY}

  # Collabora online server for nextcloud to enable document processing. Reference: https://hub.docker.com/r/collabora/code
  # https://cloud.thesysadminhub.com/s/FNKyP43y35HGDTJ?dir=/
  # https://docs.nextcloud.com/server/28/admin_manual/office/example-docker.html#install-the-collabora-online-server
  collabora:
    image: collabora/code:latest
    hostname: collabora
    container_name: collabora
    restart: unless-stopped
    environment:
      domain: ${COLLABORA_FQDN}
      dictionaries: en
      username: ${COLLABORA_UNAME}
      password: ${COLLABORA_PWD}
      aliasgroup1: https://${NEXTCLOUD_FQDN}:443
      extra_params: "--o:ssl.enable=false --o:ssl.termination=true"
      # keep this false when moving to CA-issued valid SSL certificates
      SKIP_CERT_VERIFY: ${SKIP_CERT_VERIFY}
    cap_add:
      - MKNOD
    ports:
      - 127.0.0.1:9980:9980
    networks:
      - default
      - proxy-tier

  # nextcloud talk server for nextcloud to enable audio/video calls. Reference: https://hub.docker.com/r/nextcloud/aio-talk
  nc-talk:
    container_name: talk_hpb
    image: ghcr.io/nextcloud-releases/aio-talk:latest
    init: true
    ports:
      - 3478:3478/tcp
      - 3478:3478/udp
      - 8081:8081/tcp
    environment:
      - NC_DOMAIN=${NEXTCLOUD_FQDN}
      - TALK_HOST=${SIGNAL_FQDN}
      - TURN_SECRET=${TURN_SECRET} #this must be a long secretpasswordkey
      - SIGNALING_SECRET=${SIGNALING_SECRET} #this must be a long secretpasswordkey
      - TZ=${TIME_ZONE}
      - TALK_PORT=3478
      - INTERNAL_SECRET=${INTERNAL_SECRET} #this must be a long secretpasswordkey
      - SKIP_CERT_VERIFY=${SKIP_CERT_VERIFY} # true for local self-signed certs; false for CA-issued valid SSL certificates
    restart: unless-stopped
    networks:
      - default
      - proxy-tier

volumes:
  db:
  nextcloud:

networks:
  proxy-tier:
```

## Nextcloud Admin settings

### Nextcloud office admin settings

- Nextcloud office settings can be found at the settings/admin/richdocuments URL or Administration settings(top right)→Administration(left menu section)→Office menu in the web UI
- Validate that configurations made the post installation script in this UI

![nextcloud%20collabora%20config%20ui.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/nextcloud%20collabora%20config%20ui.png?raw=true)

### Nextcloud talk admin settings

- Nextcloud talk settings can be foound at the /settings/admin/talk URL or Administration settings(top right)→Administration(left menu section)→Talk menu in the web UI
- Validate that configurations made the post installation script in this UI

![nextcloud%20talk%20hpb%20config%20ui.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/nextcloud%20talk%20hpb%20config%20ui.png?raw=true)

![nextcloud%20talk%20stun%20servers%20config%20ui.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/nextcloud%20talk%20stun%20servers%20config%20ui.png?raw=true)

![nextcloud%20talk%20turn%20servers%20config%20ui.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/nextcloud%20talk%20turn%20servers%20config%20ui.png?raw=true)

### Nextcloud Cron job setup

- Nextcloud required a cron job to run every 5 mins.
- One way to run the cron job is to run the command `app php /var/www/html/cron.php`
- We can configure a Linux cron job to run this command every 5 mins as shown below

```bash
sudo crontab -e
*/5 * * * * docker exec -u www-data app php /var/www/html/cron.php 
```

- A task scheduler task can also be run in windows similarly to run the cron job periodically

![nextcloud%20cron%20setup%20ui.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/nextcloud%20cron%20setup%20ui.png?raw=true)

- Nextcloud needs to be configured as shown above to “Cron” mode either in UI or by running the command `php occ background:cron`. This command can be run inside the nextcloud Docker container using the command

```bash
   docker exec -u www-data app php occ background:cron
```

### Self-signed certificate

- This docker setup uses a flag that specifies if we are using self-signed certificates for this nextcloud installation
- Use `SKIP_CERT_VERIFY=false`  if the Nextcloud setup uses CA verified ssl certificates instead of self-signed certificates

## References

- Nextcloud docker container - https://github.com/nextcloud/docker
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc1MTE4NjI4MSwtMzY0NzI5ODM1LDY3MT
U2MjI3NCwtMTU0NzMxOTI0MF19
-->