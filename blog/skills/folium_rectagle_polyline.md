## Skill - Draw Rectangle, Polyline, Polygon in python folium

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

### Draw a Rectangle with diagonal coordinates
```python
# import folium library
import folium

# create a map object
mapObj = folium.Map(location=[24.2170111233401, 81.0791015625000],
                    zoom_start=5)

# create a rectangle object and add to map
folium.Rectangle([(28.6471948,76.9531796), (19.0821978,72.7411)]).add_to(mapObj)

# save the map object as a html
mapObj.save('output.html')
```

### stroke and fill options for rectangle, polyline, polygon
* all the styling options can be found at https://leafletjs.com/reference-1.6.0.html#path . Use snake_case instead of camelCase for specifying options in python
* Some of the important styling options are
	* stroke - set to True to enable line stroke, default is True 
	* weight - line stroke width in pixels, default is 5
	* color - line stroke color
	* opacity - line stroke opacity
	* fill - set to True to enable filling with color, default is False
	* fill_color - fill Color
	* fill_opacity - ranges between 0 to 1. 0 means transparent, 1 means opaque
	* 
```python
import folium

# create a map object
mapObj = folium.Map(location=[24.2170111233401, 81.0791015625000],
                    zoom_start=5)

# create a rectangle object and add to map
folium.Rectangle([(28.6471948,76.9531796), (19.0821978,72.7411)],
                    color="green",
                    weight=2,
                    fill=True,
                    fill_color="pink",
                    fill_opacity=0.5).add_to(mapObj)

# save the map object as a html
mapObj.save('output.html')
```

### Draw a Polyline
```python
# import folium library
import folium

# create a map object
mapObj = folium.Map(location=[24.2170111233401, 81.0791015625000],
                    zoom_start=5)

# create a polyline with the coordinates
folium.PolyLine([(19.0821978, 72.7411), (28.6471948, 76.9531796), (24.2170111233401, 81.0791015625000)],
                color="red",
                weight=2).add_to(mapObj)

# save the map object as a html
mapObj.save('output.html')
```

### Draw a Polygon
```python
# import folium library
import folium

# create a map object
mapObj = folium.Map(location=[24.2170111233401, 81.0791015625000],
                    zoom_start=5)

# create a polygon with the coordinates
folium.Polygon([(19.0821978, 72.7411), (28.6471948, 76.9531796), (24.2170111233401, 81.0791015625000), (20.7021709, 76.9905048), (12.9542946, 77.490855)],
               color="blue",
               weight=2,
               fill=True,
               fill_color="orange",
               fill_opacity=0.4).add_to(mapObj)

# save the map object as a html
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

![folium_circles_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/folium_circles_demo.png)
### Video
The video for this post can be seen [here](https://youtu.be/jFaa2vwU4-M)

<iframe width="560" height="315" src="https://www.youtube.com/embed/jFaa2vwU4-M" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### References
* circle styling options - https://leafletjs.com/reference-1.7.1.html#path
* Rectangle docs - https://python-visualization.github.io/folium/modules.html#folium.vector_layers.Rectangle

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NzQyODkzNDEsMTA4MDMxNDI5MSwtMT
IyMTEzMzc2MF19
-->