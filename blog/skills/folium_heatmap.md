## Skill - Draw heatmap in python folium map

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Introduction to Folium for interactive maps in python](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will learn how to draw heatmap in **folium** maps using the heatmap plugin in the folium library. See [this](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html) post to learn about folium libary basics.

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

### Difference between a Polygon and a Polyline
The only difference is that the polygon will be a closed shape even if the (lat, long) of last mentioned coordinate is not the same as the first one.

### Keep shapes in a different layer
```python
# import folium library
import folium

# create a map object
mapObj = folium.Map(location=[24.2170111233401, 81.0791015625000],
                    zoom_start=5)

# create a layer on the map object
shapesLayer = folium.FeatureGroup(name="Vector Shapes").add_to(mapObj)

# create a rectangle object and add to map
folium.Rectangle([(28.6471948,76.9531796), (19.0821978,72.7411)]).add_to(shapesLayer)

# create a polyline with the coordinates
folium.PolyLine([(17.4126274,78.2679611), (25.6081756,85.073003), (26.4473103,80.2683428)]).add_to(shapesLayer)

# display the layer switcher widget
folium.LayerControl().add_to(mapObj)

# save the map object as a html
mapObj.save('output.html')
```

### Complete Example
```python
# import folium library
import folium

# create a map object
mapObj = folium.Map(location=[22.64443248121717, 79.80468750000001],
                    zoom_start=6)

# create a layer on the map object
shapesLayer = folium.FeatureGroup(name="Vector Shapes").add_to(mapObj)

# create a rectangle object and add to map
folium.Rectangle(
    [(28.0214793, 73.2845211), (22.7241158, 75.7938099)],
    weight=2,
    fill_color="orange",
    fill_opacity=0.4).add_to(shapesLayer)

# create a polyline with the coordinates
folium.PolyLine([(28.5274851, 77.1389452), (27.1763098, 77.9099731), (23.199552, 77.3358515),
                 (21.1612315, 79.0024702), (17.661548, 75.8835978)],
                color="green",
                weight=4).add_to(shapesLayer)

# create a polygon with the coordinates
folium.Polygon([(25.4024022, 81.7315446), (25.6081756, 85.073003), (20.4631843, 85.8327264),
                (19.0860155, 82.0161332), (21.4692684, 80.1817197)],
               weight=2,
               color="red",
               fill_color="yellow",
               fill_opacity=0.3).add_to(shapesLayer)

# display the layer switcher widget
folium.LayerControl().add_to(mapObj)

# save the map object as a html
mapObj.save('output.html')
```

![folium_rectangle_polygon_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/folium_rectangle_polygon_demo.png)

<hr/>

### References
* styling options - https://leafletjs.com/reference-1.7.1.html#path
* Rectangle docs - https://python-visualization.github.io/folium/modules.html#folium.vector_layers.Rectangle
* Polygon docs - https://python-visualization.github.io/folium/modules.html#folium.vector_layers.Polygon
* Polyline docs - https://python-visualization.github.io/folium/modules.html#folium.vector_layers.PolyLine

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)





> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTg4NjY0MDFdfQ==
-->