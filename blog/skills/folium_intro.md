## Skill - Introduction to Folium for interactive maps in python
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will get a beginner level introduction to Folium library which is extensively **used for creating interactive maps** in python

### Topics covered
* Initialize a folium map object with map center and zoom
* Layer controls button to show/hide layers
* Create tile layers from built-in sources
* Create tile layers from other sources
* Save a map object as html file

### Installing folium
* Open command prompt and type ```python -m pip install folium```
![pip install folium](https://github.com/nagasudhirpulla/taming_python/raw/0aadac449b8f8e1b0a8659c79f32b3798aef991b/blog/skills/assets/img/folium_pip_install.png)
### Initialize a folium map object with map center and zoom
Lets create a simple folium map object
```python
import folium
mapObj = folium.Map(location=[21.437730075416685, 77.255859375],
zoom_start=2, tiles='OpenStreetMap')
```

* Keep ```tiles=None``` to create a map without tiles
* The options for tile sources in folium can be found [here](http://python-visualization.github.io/folium/modules.html#folium.raster_layers.TileLayer)

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
                     zoom_start=4, tiles=None)

# add tile layers
folium.TileLayer('openstreetmap').add_to(mapObj)
folium.TileLayer('stamenterrain', attr="stamenterrain").add_to(mapObj)
folium.TileLayer('stamenwatercolor', attr="stamenwatercolor").add_to(mapObj)
folium.TileLayer('https://{s}.basemaps.cartocdn.com/dark_all/{z}/{x}/{y}{r}.png', name='CartoDB.DarkMatter', attr="CartoDB.DarkMatter").add_to(mapObj)

# add layers control over the map
folium.LayerControl().add_to(mapObj)

# save the map as html file
mapObj.save('folium_intro.html')
```

<hr/>

### References
* folium quickstart - https://python-visualization.github.io/folium/quickstart.html
* folium official docs - http://python-visualization.github.io/folium/modules.html#
* leaflet js - https://leafletjs.com/index.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk2NTA0MDQ2Nyw4NDYyNjI0NjgsNDI0MT
kwNTg5LDQ3NDkzMDIyNSwxODkyOTIwNDksLTE4MjczNDE4NjZd
fQ==
-->