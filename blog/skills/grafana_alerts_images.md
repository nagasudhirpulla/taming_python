# Grafana alert emails with images
Images can be embedded in Grafana alerts using the Grafana Image Renderer Plugin

![grafana_alert_email_image_demo.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana_alert_email_image_demo.png?raw=true)

## How it works

-   Grafana uses chromium (a headless browser) to render Grafana panels to PNG files
-   The plugin comes with chromium and Node JS installed, so separate installation of these dependencies is not required

## Installation

### Install from command line in Grafana folder

-   Open a command line in the Grafana bin folder and then run the following command

```powershell
grafana-cli.exe plugins install grafana-image-renderer

```

-   This command downloads plugin from internet and keeps it in the grafana→data→plugins folder of Grafana installation

### Install offline

-   Download the zip file from GitHub at [https://github.com/grafana/grafana-image-renderer/releases](https://github.com/grafana/grafana-image-renderer/releases)
-   Check Grafana version compatibility while downloading
-   unzip the plugin files in the grafana→data→plugins folder of Grafana installation (For example “C:\Program Files\GrafanaLabs\data\plugins")

## Configure Grafana Image renderer

-   In the defaults.ini file [unified_alerting.screenshots] section, keep `cature = true`
-   Some settings are also present in the [plugin.grafana-image-renderer] section of the defaults.ini Grafana config file’s (Example: “C:\Program Files\GrafanaLabs\grafana\conf\defaults.ini”)
-   The plugin.json file present in the plugins folder (Example: C:\Program Files\GrafanaLabs\data\plugins\grafana-image-renderer\plugin.json") can be used for plugin configuration

## Link Dashboard in Alert

-   After setting up Grafana Image Renderer, Grafana dashboard panel should be linked in the alert rule as shown below for the image to be created for email

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2127588-bc2c-4960-9072-182c822d4772/8fc79dec-c8c4-43b2-8d43-a6fec0ffc727/Untitled.png)

## Setup Remote rendering service

-   Grafana Image renderer plugin renders the images itself by default using the chromium browser bundled with it
-   But the plugin can also use a remote rendering service to offload the job of image rendering. This can be useful when the server running Grafana has some missing dependencies or incompatibilities.
-   Create a remote rendering server using the following steps
    -   Clone the [Grafana image renderer plugin](https://github.com/grafana/grafana-image-renderer/) Git repository.
        
    -   Install dependencies and build:
        
        ```bash
        yarn install --pure-lockfile
        yarn run build
        
        ```
        
    -   Run the server on a desired port:
        
        ```bash
        node build/app.js server --port=8081
        
        ```
        
    -   Update Grafana configuration to mention the details of the remote rendering service:
        
        ```bash
        [rendering]
        server_url = <http://localhost:8081/render>
        callback_url = <http://localhost:3000/>
        
        ```
        
    -   Restart Grafana.
        

## References

-   Grafana image rendering plugin documentation - [https://grafana.com/docs/grafana/latest/setup-grafana/image-rendering/](https://grafana.com/docs/grafana/latest/setup-grafana/image-rendering/)
-   unified alerting screenshots configuration - [https://grafana.com/docs/grafana/latest/setup-grafana/configure-grafana/#unified_alertingscreenshots](https://grafana.com/docs/grafana/latest/setup-grafana/configure-grafana/#unified_alertingscreenshots)
-   Grafana remote rendering service - [https://github.com/grafana/grafana-image-renderer?tab=readme-ov-file#remote-rendering-service-installation](https://github.com/grafana/grafana-image-renderer?tab=readme-ov-file#remote-rendering-service-installation)
<!--stackedit_data:
eyJoaXN0b3J5IjpbODg0OTYwNTQyLC03NTUyMzU1OF19
-->