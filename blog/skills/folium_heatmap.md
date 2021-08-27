## Skill - Draw heatmap on a python folium map

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

folium heatmap plugin documentation can be found [here](http://python-visualization.github.io/folium/plugins.html#folium.plugins.HeatMap)

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

### Values to be provided
* While providing the values to heatmap, re-scale the input values so that they range between 0 and 1
* 0 corresponds to least intensity, 1 corresponds to highest intensity

### Values to colors mapping using the "gradient" input
By providing a dictionary to the ```gradient``` input of the heatmap, the values to color mapping can be configured
```python
import folium
from folium.plugins import HeatMap

# create a map object
mapObj = folium.Map([24.21, 81.08], zoom_start=6)

# data for heatmap.
# each list item should be in the format [lat, long, value]
data = [
    [24.399, 80.142, 77],
    [22.252, 80.885, 50],
    [23.751, 79.995, 98],
]

# rescale each value between 0 and 1 using (val-minColorVal)/(maxColorVal-minColorVal)
# here minColorVal = 50 and maxColorVal = 100
mapData = [[x[0], x[1], (x[2]-50)/(100-50)] for x in data]

# custom color gradient
colrGradient = {0.0: 'blue',
                0.6: 'cyan',
                0.7: 'lime',
                0.8: 'yellow',
                1.0: 'red'}

# create heatmap from the data and add to map
HeatMap(mapData, gradient=colrGradient).add_to(mapObj)

# save the map object as html
mapObj.save("output.html")
```

![folium_heatmap_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/folium_heatmap_demo.png)

<hr/>

### References
* heatmap plugin documentation - http://python-visualization.github.io/folium/plugins.html#folium.plugins.HeatMap
* default heatmap gradient colors dictionary - https://github.com/mourner/simpleheat/blob/c1998c36fa2f9a31350371fd42ee30eafcc78f9c/simpleheat.js#L22

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMTU0NDg1NDIsLTEyNTgwNTgyNjUsMT
kxMjc3NzE0NywtMTczNjMyNzk0MywtNzkxMzkxNjM1LDkxNTY0
NjQyMiwtMTg5ODQ4NDcyNCw5ODg2NjQwMV19
-->