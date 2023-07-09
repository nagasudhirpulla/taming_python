## Animated lines in python folium maps

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Prerequisites
* [Introduction to Folium for interactive maps in python](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html)

<hr/>

In this post we will learn how to draw animated lines with moving ants animation effect in python folium maps using **antpath** plugin of folium python module


```python
import folium
from folium.plugins import AntPath

# create a map object
mapObj = folium.Map(location=[18.906286495910905, 79.40917968750001],
                    zoom_start=5)

# latitude longitude coordinates of the lines
pathLatLngs = [(19.082502,72.7163773), (12.9541467,77.3191065), (23.199546,77.3234906), (19.0860154,82.0145882), (22.5355649,88.2649519)]
pathLatLngs2 = [(13.0478078,80.0442025), (17.6615468,75.8774177), (24.6083586,73.6636725), (26.8488213,80.860112)]

# create antpaths and add to map
AntPath(pathLatLngs, delay=400, dash_array=[30,15], color="red", weight=3).add_to(mapObj)

AntPath(pathLatLngs2, delay=200, dash_array=[10,50], color="blue", pulse_color="orange", weight=5, opacity=1).add_to(mapObj)

# save the map object as a html
mapObj.save('output.html')

```

-   As shown in the above code, using “Antpath” class, antpath objects can be created and added to map object
-   Some of the parameters of the antpath line are
    -   delay - configures speed to animation, smaller value will increase speed
    -   color - color of the line
    -   pulse_color - color of the moving ants on the line
    -   weight - thickness of the line
    -   opacity - sets the transparency of the line, 1 means no transparency
    -   dash_array - the first number determines the length of each ant and the second number determines the distance between 2 ants
-   The configuration options can be interactively previewed at [https://rubenspgcavalcante.github.io/leaflet-ant-path/](https://rubenspgcavalcante.github.io/leaflet-ant-path/)

![folium_antpath_demo.gif](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/folium_antpath_demo.gif?raw=true)

### Video
The video for this post can be seen [here](https://youtu.be/pDRN3ORUi0o)

<iframe width="560" height="315" src="https://www.youtube.com/embed/pDRN3ORUi0o" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


## References

-   folium antpath plugin docs - [https://python-visualization.github.io/folium/plugins.html#folium.plugins.AntPath](https://python-visualization.github.io/folium/plugins.html#folium.plugins.AntPath)
-   Antpath github page - [https://github.com/rubenspgcavalcante/leaflet-ant-path](https://github.com/rubenspgcavalcante/leaflet-ant-path)
-   Antpath interactive configuration options page - [https://rubenspgcavalcante.github.io/leaflet-ant-path/](https://rubenspgcavalcante.github.io/leaflet-ant-path/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM5ODUzMDU4MSw1ODAwNjU4MTUsLTEyNz
I5Mjc2ODksLTE3NDYxOTE5MDYsLTIwODg3NDY2MTJdfQ==
-->