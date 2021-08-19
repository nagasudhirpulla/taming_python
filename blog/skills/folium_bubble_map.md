
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
## Solution
The whole program can be broken down into the following tasks
* Read all the power plants information from excel file using pandas
* Create a simple map with a desired map center and map zoom 
* Draw country borders using folium.GeoJson layer
* Using folium FeatureGroup, create a map layer on which circles will be drawn
* Iterate through each power plant and draw a circle on the map. The color of the circle will be based on the fuel type of the power plant (Solar-red, Wind-blue)
* Inject HTML into the map to create a legend at the bottom left
* Create a layer switcher control for switching ON and OFF the layers

### Code
```python
import folium

mapObj = folium.Map(location=[23.294059708387206, 78.26660156250001], zoom_start=6)

folium.Circle(location=[23.294059708387206, 78.26660156250001],
              radius=50000
              ).add_to(mapObj)

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
eyJoaXN0b3J5IjpbMTQ3MDcyNDQwOCwtMTI2Njk1OTg2NiwtMT
Q0MTI5NjYyMSwzMDg5NTI3NzQsMTAzMTA0NTkwMCwxNzIwNTI5
ODcyLC04Mzc4OTIzMDZdfQ==
-->