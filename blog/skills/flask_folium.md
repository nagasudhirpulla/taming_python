## Render folium maps in python flask server

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Prerequisites
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Flask python module introduction](https://nagasudhir.blogspot.com/2022/04/flask-python-module-introduction-for.html)
* [Serve static files in flask](https://nagasudhir.blogspot.com/2022/04/serve-static-files-in-flask.html)

<hr/>


-   Folium maps can be served from python flask web applications

## Components required for a folium map

### script and style tags for linking dependencies

This script and style tags required to be placed in the HTML head tag can be rendered using `mapObj.get_root().header.render()`, where `mapObj` is the python map object

![flask_folium_head_component.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/flask_folium_head_component.png?raw=true)

### div for map container

The HTML div container of the map can be rendered in the HTML body using `mapObj.get_root().html.render()`
![flask_folium_body_component.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/flask_folium_body_component.png?raw=true)

### JavaScript for initializing and rendering the map

![flask_folium_script_component.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/flask_folium_script_component.png?raw=true)

The JavaScript required to initialize and render the folium map can be rendered in the HTML script tag using `m.get_root().script.render()`

## Example

```python
from flask import Flask, render_template_string
import folium

# create a flask application
app = Flask(__name__)

@app.route("/")
def home():
    """Create a map object"""
    mapObj = folium.Map(location=[18.906286495910905, 79.40917968750001],
                        zoom_start=5, width=800, height=500)

    # add a marker to the map object
    folium.Marker([17.4127332, 78.078362],
                  popup="<i>This a marker</i>").add_to(mapObj)

    # render the map object
    mapObj.get_root().render()

    # derive the script and style tags to be rendered in HTML head
    header = mapObj.get_root().header.render()

    # derive the div container to be rendered in the HTML body
    body_html = mapObj.get_root().html.render()

    # derive the JavaScript to be rendered in the HTML body
    script = mapObj.get_root().script.render()

    # return a web page with folium map components embeded in it. You can also use render_template.
    return render_template_string(
        """
            <!DOCTYPE html>
            <html>
                <head>
                    {{ header|safe }}
                </head>
                <body>
                    <h1>Embed folium map in HTML page</h1>
                    {{ body_html|safe }}
                    <h3>This map is embeded in a flask server web page !</h3>
                    <script>
                        {{ script|safe }}
                    </script>
                </body>
            </html>
        """,
        header=header,
        body_html=body_html,
        script=script,
    )

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=50100, debug=True)

```

![flask_folium_embed_example.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/flask_folium_embed_example.png?raw=true)

## Render map in an iframe

-   `m.get_root()._repr_html_()` can be used to render the map in an iframe of a webpage

```python
from flask import Flask, render_template_string
import folium

# create a flask application
app = Flask(__name__)

@app.route("/")
def home():
    """Create a map object"""
    mapObj = folium.Map(location=[18.906286495910905, 79.40917968750001],
                        zoom_start=5)

    # add a marker to the map object
    folium.Marker([17.4127332, 78.078362],
                  popup="<i>This a marker</i>").add_to(mapObj)

    # set iframe width and height
    mapObj.get_root().width = "700px"
    mapObj.get_root().height = "500px"

    # derive the iframe content to be rendered in the HTML body
    iframe = mapObj.get_root()._repr_html_()

    # return a web page with folium map components embeded in it. You can also use render_template.
    return render_template_string(
        """
            <!DOCTYPE html>
            <html>
                <head></head>
                <body>
                    <h1>Using iframe to render folium map in HTML page</h1>
                    {{ iframe|safe }}
                    <h3>This map is place in an iframe of the page!</h3>
                </body>
            </html>
        """,
        iframe=iframe,
    )

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=50100, debug=True)

```

-   When the map is rendered in an iframe, the webpage cannot interact with the map via JavaScript

### Video
The video for this blog can be seen [here](https://youtu.be/zctCsvSSYu8)



## References

-   [https://python-visualization.github.io/folium/flask.html#:~:text=A common use case is,map components and use those](https://python-visualization.github.io/folium/flask.html#:~:text=A%20common%20use%20case%20is,map%20components%20and%20use%20those).
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc5Njc0Njk1MCwtODM0MzU3ODM4LDUwNT
kzNDEzXX0=
-->