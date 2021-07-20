## Skill - Draw circles and circle markers in python folium

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Introduction to Folium for interactive maps in python](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will learn how to draw circles in **folium** maps. See [this](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html) post to learn about folium libary basics

### Draw a simple circle with location and radius
* location - latitude, longitude location of the center of the circle
* radius - radius of the circle in **meters**
```python
import folium

mapObj = folium.Map(location=[23.294059708387206, 78.26660156250001], zoom_start=6)

folium.Circle(location=[23.294059708387206, 78.26660156250001],
              radius=50000
              ).add_to(mapObj)

mapObj.save('output.html')
```

### Circle stroke and fill options
* all the styling options can be found at https://leafletjs.com/reference-1.6.0.html#path . Use snake_case instead of camelCase for specifying options in python
* Some of the important styling options are
	* stroke - set to True to enable line stroke, default is True 
	* weight - line stroke width in pixels, default is 5
	* color - line stroke color
	* opacity - line stroke opacity
	* fill - set to True to enable filling with color, default is False
	* fill_color - fill Color
	* fill_opacity - ranges between 0 to 1. 0 means transparent, 1 means opaque
```python
import folium

mapObj = folium.Map(location=[23.294059708387206, 78.26660156250001], zoom_start=6)

folium.Circle(location=[23.294059708387206, 78.26660156250001],
              radius=50000,
              color='green',
              weight=6,
              fill_color='red',
              fill_opacity = 0.5
              ).add_to(mapObj)

mapObj.save('output.html')
```

### Circle with tooltip and popup
```python
import folium

mapObj = folium.Map(location=[23.294059708387206, 78.26660156250001], zoom_start=6)

folium.Circle(location=[23.294059708387206, 78.26660156250001],
              radius=50000,
              fill=True,
              tooltip="This is a tooltip text",
              popup=folium.Popup("""<h2>This is a popup</h2><br/>
              This is a <b>new line</b><br/>
              <img src="https://www.w3schools.com/html/pic_trulli.jpg" alt="Trulli" style="max-width:100%;max-height:100%">""", max_width=500)
              ).add_to(mapObj)

mapObj.save('output.html')
```

### Keep shapes in different layer
```python
from os import name
import folium

mapObj = folium.Map(location=[23.294059708387206, 78.26660156250001], zoom_start=6)

# create a layer on the map object
shapesLayer = folium.FeatureGroup(name="circles").add_to(mapObj)

folium.Circle(location=[23.294059708387206, 78.26660156250001],
              radius=50000,
              fill=True
              ).add_to(shapesLayer)

folium.LayerControl().add_to(mapObj)

mapObj.save('output.html')
```

### Complete example
```python
import folium

mapObj = folium.Map(location=[23.294059708387206, 78.26660156250001],
                    zoom_start=5)

shapesLayer = folium.FeatureGroup(name="circles").add_to(mapObj)

folium.Circle(location=[23.294059708387206, 78.26660156250001],
              weight=1,
              radius=50000,
              fill_color='pink',
              tooltip="Tooltip text",
              popup=folium.Popup("""<h2>This is a popup</h2><br/>
              This is a <b>new line</b><br/>
              <img src="https://www.w3schools.com/html/pic_trulli.jpg" alt="Trulli" style="max-width:100%;max-height:100%">""", max_width=500)
              ).add_to(shapesLayer)

folium.LayerControl().add_to(mapObj)

mapObj.save('output.html')
```

![folium_geojson_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/folium_geojson_demo.png)
### Video
The video for this post can be seen [here](https://youtu.be/h16O4xt6yBU)

<iframe width="560" height="315" src="https://www.youtube.com/embed/h16O4xt6yBU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### References
* what is GeoJSON - https://en.wikipedia.org/wiki/GeoJSON
* GeoJSON styling options - https://leafletjs.com/reference-1.7.1.html#path
* official docs - https://python-visualization.github.io/folium/modules.html#folium.features.GeoJson

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgwMzczODM2NCwtMTcxOTYyNDAzOSwzNz
QxODk4NzUsMTY2OTkxODU2OF19
-->