## Skill - Marker Clusters on a python folium map

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Introduction to Folium for interactive maps in python](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html)
* [Draw markers in python folium maps](https://nagasudhir.blogspot.com/2021/07/draw-markers-in-python-folium-maps.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will learn how to create a marker cluster in **folium** maps using the MarkerCluster plugin in the folium library. See [this](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html) post to learn about folium libary basics.

folium Marker Cluster plugin documentation can be found [here](https://python-visualization.github.io/folium/plugins.html#folium.plugins.MarkerCluster)

### Code
```python
import folium
from folium.plugins import MarkerCluster
import random

# create a map object
mapObj = folium.Map([24.21, 81.08], zoom_start=6)

# creating random marker locations for Marker Cluster.
# each list item should be in the format [lat, long]
markerLocs = [[random.uniform(18, 29), random.uniform(73, 85)]
              for x in range(100)]

mCluster = MarkerCluster(name="Markers Demo").add_to(mapObj)

for pnt in markerLocs:
    folium.Marker(location=[pnt[0], pnt[1]],
                  popup="pnt - {0}, {1}".format(pnt[0], pnt[1])).add_to(mCluster)

folium.LayerControl().add_to(mapObj)

# save the map object as html
mapObj.save("output.html")
```
### Points to remember
* By mentioning the ```name``` input to the ```MarkerCluster``` function, we can control the name of the Marker Cluster layer in Layer switcher


![marker_cluster_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/marker_cluster_demo.png)
### Video
The video for this post can be found [here](https://youtu.be/n7HUBNmXB5Y)
<iframe width="560" height="315" src="https://www.youtube.com/embed/n7HUBNmXB5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### References
* MarkerCluster plugin documentation - https://python-visualization.github.io/folium/plugins.html#folium.plugins.MarkerCluster

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NTQ4NDUwNTgsLTc3NTYyMTQ0MiwtNz
g2OTU4ODMxLDE2MjAwMzU0MTMsMTkwNzAzMTIxNywtMTcxMjAz
NjQ0NV19
-->