
## Challenge - Create a bubble map from excel data using python folium and pandas

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [pandas DataFrame Basics](https://nagasudhir.blogspot.com/2020/05/pandas-dataframe-basics.html)
* [Working with excel files and pandas DataFrames](https://nagasudhir.blogspot.com/2020/05/working-with-excel-and-pandas-dataframes.html)
* [Introduction to Folium for interactive maps in python](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html)
* [Draw borders from GeoJSON paths in python folium maps](https://nagasudhir.blogspot.com/2021/07/draw-borders-from-geojson-paths-in.html)
* [Draw circles and circle markers in python folium](https://nagasudhir.blogspot.com/2021/07/draw-circles-and-circle-markers-in.html)
* [Inject HTML into python folium maps](https://nagasudhir.blogspot.com/2021/08/inject-html-into-python-folium-maps.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will learn how to draw a bubble map from excel data using **pandas** and **folium** python libraries

## Challenge
* Plot the capacities of power plants provided in an excel file on a geographical bubble map
* The bubbles of wind plants will be blue and bubbles of solar plants will be red
* When user clicks on a bubble, it's information should be shown on a popup
* There should be legend at the bottom left of the map for explaining the bubble colors
![bubble_map_demo_data](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/bubble_map_demo_data.png)
The whole program can be broken down into the following tasks
* Read all the power plants information from excel file using pandas
* Create a simple map with a desired map center and map zoom 
* Draw borders using folium.GeoJson layer
* Using folium FeatureGroup, create a map layer on which circles will be drawn
* Iterate through each power plant and draw a circle on the map. The color of the circle will be based on the fuel type of the power plant (Solar-red, Wind-blue)
* Inject HTML into the map to create a legend at the bottom left
* Create a layer switcher control for switching ON and OFF the layers

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

### Difference between Circle and CircleMarker
The radius in Circle is defined in **meters**, where as the radius in CircleMarker is defined in **pixels**
```python
import folium

mapObj = folium.Map(location=[23.294059708387206, 78.26660156250001], zoom_start=6)

folium.CircleMarker(location=[23.294059708387206, 78.26660156250001],
              radius=50
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
                    zoom_start=6)

shapesLayer = folium.FeatureGroup(name="circles").add_to(mapObj)

circlesData = [
    [25, 74, 80000],
    [22, 79, 60000],
    [26, 82, 90000]
]

for cData in circlesData:
    folium.Circle(location=[cData[0], cData[1]],
                  radius=cData[2],
                  weight=5,
                  color='green',
                  fill_color='red',
                  tooltip="Tooltip text",
                  popup=folium.Popup("""<h2>This is a popup</h2><br/>
                    This is a <b>new line</b><br/>
                    <img src="https://www.w3schools.com/html/pic_trulli.jpg" alt="Trulli" style="max-width:100%;max-height:100%">""", max_width=500)
                  ).add_to(shapesLayer)

folium.LayerControl().add_to(mapObj)

mapObj.save('output.html')
```

![bubble_map_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/bubble_map_demo.png)
### Video
The video for this post can be seen [here](https://youtu.be/jFaa2vwU4-M)

<iframe width="560" height="315" src="https://www.youtube.com/embed/jFaa2vwU4-M" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### References
* circle styling options - https://leafletjs.com/reference-1.7.1.html#path
* circle docs - https://python-visualization.github.io/folium/modules.html#folium.vector_layers.Circle
* circle marker docs - https://python-visualization.github.io/folium/modules.html#folium.vector_layers.CircleMarker

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMzg2NTMxNTUsMzA4OTUyNzc0LDEwMz
EwNDU5MDAsMTcyMDUyOTg3MiwtODM3ODkyMzA2XX0=
-->