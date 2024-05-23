# Grafana alert emails with images
Images can be embedded in Grafana alerts using the **Grafana Image Renderer** Plugin

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

-   In the defaults.ini file [unified_alerting.screenshots] section, keep `capture = true`
-   Some settings are also present in the [plugin.grafana-image-renderer] section of the defaults.ini Grafana config file’s (Example: “C:\Program Files\GrafanaLabs\grafana\conf\defaults.ini”)

## Link Dashboard in Alert

-   After setting up Grafana Image Renderer, Grafana dashboard panel should be linked in the alert rule as shown below for the image to be created for email

![grafana_alert_panel_link_demo.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/grafana_alert_panel_link_demo.png?raw=true)
## Debug image rendering problems
* Grafana logs can be super useful to check if Grafana Image Renderer plugin is running without any problems
* Open the `grafana.log` file in the grafana→data→log folder of Grafana installation (For example “C:\Program Files\GrafanaLabs\data\log")
* Search for "grafana-image-renderer" in the `grafana.log` file to see the logs related to the plugin

## Setup remote rendering service

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
        server_url = http://localhost:8081/render
        callback_url = http://localhost:3000/
        
        ```
        
    -   Restart Grafana.

### Video
Video on this post can be seen [here](https://youtu.be/tP_uO92ykUU?si=eHFhRi54QCEXitlj)

<iframe width="560" height="315" src="https://www.youtube.com/embed/tP_uO92ykUU?si=eHFhRi54QCEXitlj" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## References

-   Grafana image rendering plugin documentation - [https://grafana.com/docs/grafana/latest/setup-grafana/image-rendering/](https://grafana.com/docs/grafana/latest/setup-grafana/image-rendering/)
-   unified alerting screenshots configuration - [https://grafana.com/docs/grafana/latest/setup-grafana/configure-grafana/#unified_alertingscreenshots](https://grafana.com/docs/grafana/latest/setup-grafana/configure-grafana/#unified_alertingscreenshots)
-   Grafana remote rendering service - [https://github.com/grafana/grafana-image-renderer?tab=readme-ov-file#remote-rendering-service-installation](https://github.com/grafana/grafana-image-renderer?tab=readme-ov-file#remote-rendering-service-installation)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjkxNjQwMTA5LDIyNzA2NTAxNywxNTU5Mz
k2NDkzLDE5Mjc5NjE5MjEsLTE3NzY1MzU2MTUsLTc1NTIzNTU4
XX0=
-->