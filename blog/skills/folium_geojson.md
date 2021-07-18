## Skill - Draw borders from GeoJSON paths in python folium maps

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Introduction to Folium for interactive maps in python](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will learn how to draw GeoJSON paths in **folium** maps. See [this](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html) post to learn about folium libary basics

### Files used in this example
Place the following files in the same folder of the python file to run this code example
* [states_india.geojson](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/states_india.geojson)
* [srilanka.geojson](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/srilanka.geojson)

### Create map layer with geojson data
```python
import folium

mapObj = folium.Map()

layer1 = folium.GeoJson(
data=(open("states_india.geojson", 'r').read()),
name="India")
layer1.add_to(mapObj)
```

### Layer controls button to show/hide layers
```python
import folium
mapObj = folium.Map()

# add layers control over the map
folium.LayerControl().add_to(mapObj)
```

### Create tile layers from built-in sources
```python
import folium
mapObj = folium.Map()

# add new tile layers
folium.TileLayer('openstreetmap').add_to(mapObj)
folium.TileLayer('stamenterrain', attr="stamenterrain").add_to(mapObj)
folium.TileLayer('stamenwatercolor', attr="stamenwatercolor").add_to(mapObj)

# add layers control over the map
folium.LayerControl().add_to(mapObj)
```

The options for built-in tile sources in folium can be found [here](http://python-visualization.github.io/folium/modules.html#folium.raster_layers.TileLayer)

### Create tile layers from other sources
```python
import folium
mapObj = folium.Map()

# add new tile layer from external source
folium.TileLayer('https://{s}.basemaps.cartocdn.com/dark_all/{z}/{x}/{y}{r}.png', name='CartoDB.DarkMatter', attr="CartoDB.DarkMatter").add_to(mapObj)

# add layers control over the map
folium.LayerControl().add_to(mapObj)
```
The options for external tile sources can be explored [here](http://leaflet-extras.github.io/leaflet-providers/preview/)

### Save a map object as html file
```python
import folium
mapObj = folium.Map()

# save the map object as a html file
mapObj.save('folium_intro.html')
```

### Complete example
```python
import folium

# initialize a map with center and zoom
mapObj = folium.Map(location=[21.437730075416685, 77.255859375],
                    zoom_start=7,
                    tiles=None)
# folium.TileLayer('stamenterrain', attr="stamenterrain").add_to(mapObj)

# show borders
# style options - https://leafletjs.com/reference-1.7.1.html#path
bordersStyle = {
    'color': 'green',
    'weight': 2,
    'fillColor': 'blue',
    'fillOpacity': 0.2
}
indiaLayer = folium.GeoJson(
    data=(open("states_india.geojson", 'r').read()),
    name="India",
    style_function=lambda x: bordersStyle)
indiaLayer.add_to(mapObj)

srilankaLayer = folium.GeoJson(
    data=(open("srilanka.geojson", 'r').read()),
    name="Srilanka",
    style_function=lambda x: bordersStyle)
srilankaLayer.add_to(mapObj)

# add layer control over the map
folium.LayerControl().add_to(mapObj)

# save the map as html file
mapObj.save('output.html')
```

### Video
The video for this post can be seen [here](https://youtu.be/2Mn6IvzUKvY)

<iframe width="560" height="315" src="https://www.youtube.com/embed/2Mn6IvzUKvY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### References
* what is GeoJSON - https://en.wikipedia.org/wiki/GeoJSON

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAxMTM5Mjk3MiwtMTg2NTc4NTYyNyw1MT
IzODIzNzRdfQ==
-->