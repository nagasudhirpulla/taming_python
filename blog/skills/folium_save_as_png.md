## Skill - Save folium map as png using selenium browser automation

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Introduction to Folium for interactive maps in python](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will learn how to save folium map as a pang image using selenium browser automation.

 See [this](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html) post to learn about folium libary basics

### Prerequisites - Selenium setup
In order to perform browser automation for this task we need the following components
* selenium python module - This can be installed using the command ```python -m pip install selenium```
* Gecko driver - This required to be installed in 


### Files used in this example
Place the following files in the same folder of the python file to run this code example
* [states_india.geojson](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/states_india.geojson)
* [srilanka.geojson](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/srilanka.geojson)

### Create map layer with geojson data
```python
import folium

mapObj = folium.Map(location=[22.167057857886153, 82.44140625000001], zoom_start=5)

layer1 = folium.GeoJson(
    data=(open("states_india.geojson", 'r').read()),
    name="India")
layer1.add_to(mapObj)

mapObj.save('output.html')
```

You can add multiple GeoJSON layers to a map

### Control border and fill style of GeoJSON objects

* use the ```style_function``` input of ```folium.GeoJSON``` function to control the styling of the paths.
* ```style_function``` should be a function that returns a dictionary with styling properties specified in the documentation [here](https://leafletjs.com/reference-1.7.1.html#path)
* Some of the important styling properties are
	* color - line stroke color
	* weight - line stroke width in pixels
	* opacity - line stroke opacity
	* fillColor - fill Color
	* fillOpacity - ranges between 0 to 1. 0 means transparent, 1 means opaque
```python
import folium

mapObj = folium.Map(location=[22.167057857886153, 82.44140625000001], zoom_start=5)

# style options - https://leafletjs.com/reference-1.7.1.html#path
bordersStyle = {
    'color': 'green',
    'weight': 2,
    'fillColor': 'blue',
    'fillOpacity': 0.2
}

folium.GeoJson(
    data=(open("states_india.geojson", 'r').read()),
    name="India",
    style_function=lambda x: bordersStyle).add_to(mapObj)

mapObj.save('output.html')
```

### Complete example
```python
import folium

# initialize a map with center and zoom
mapObj = folium.Map(location=[22.167057857886153, 82.44140625000001],
                    zoom_start=5)

# https://leafletjs.com/reference-1.7.1.html#path
# border styles dictionary
bordersStyle = {
    'color': 'green',
    'weight': 2,
    'fillColor': 'blue',
    'fillOpacity': 0.2
}

folium.GeoJson(
    data=(open("states_india.geojson", 'r').read()),
    name="India",
    style_function=lambda x: bordersStyle).add_to(mapObj)

folium.GeoJson(
    data=(open("srilanka.geojson", 'r').read()),
    name="Srilanka",
    style_function=lambda x: bordersStyle).add_to(mapObj)

# add layer control over the map
folium.LayerControl().add_to(mapObj)

# save the map as html file
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
eyJoaXN0b3J5IjpbLTM2ODEzODgwMiw4ODUwNDczNDhdfQ==
-->