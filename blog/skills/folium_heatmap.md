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

### Simple heatmap example
```python
import folium
from folium.plugins import HeatMap

# create a map object
mapObj = folium.Map([24.2170111233401, 81.0791015625000], zoom_start=6)

# data for heatmap. 
# each list item should be in the format [lat, long, value]
data = [
    [24.399, 80.142, 0.78],
    [22.252, 80.885, 0.68],
    [24.311, 80.543, 0.58],
    [23.195, 82.994, 0.46],
    [23.431, 80.427, 0.76],
    [26.363, 81.791, 1.81],
    [22.942, 83.257, 0.75],
    [23.751, 79.995, 0.16],
    [23.215, 81.004, 0.64],
    [24.541, 79.889, 0.55]
]

# create heatmap from the data and add to map
HeatMap(data).add_to(mapObj)

# save the map object as html
mapObj.save("output.html")
```

### mapping values to colors using the gradient input
Provide a dictionary as a ```gradient``` input to the heatmap function
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
* heatmap plugin documentation - http://python-visualization.github.io/folium/plugins.html#folium.plugins.HeatMap
* default heatmap gradient colors dictionary - https://github.com/mourner/simpleheat/blob/c1998c36fa2f9a31350371fd42ee30eafcc78f9c/simpleheat.js#L22

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)





> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MzYxMjY3OTksOTE1NjQ2NDIyLC0xOD
k4NDg0NzI0LDk4ODY2NDAxXX0=
-->