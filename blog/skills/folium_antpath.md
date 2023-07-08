## Animated lines in python folium maps

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Prerequisites
* [Introduction to Folium for interactive maps in python](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html)

<hr/>

In this post we will learn how to draw animated lines in python folium maps using **antpath** plugin of folium python module

## Challenge
* Plot the capacities of power plants provided in an excel file on a geographical bubble map
* The bubbles of wind plants will be blue and bubbles of solar plants will be red
* When user clicks on a bubble, it's information should be shown on a popup
* There should be legend at the bottom left of the map for explaining the bubble colors
![bubble_map_demo_data](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/bubble_map_demo_data.png)
### Files
* Power plants excel file can be found [here](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/power_plants.xlsx)
* Country borders GeoJson file can be found [here](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/states_india.geojson)

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
import pandas as pd
import folium

# read excel data as dataframe
dataDf = pd.read_excel('power_plants.xlsx')

# initialize a map with center and zoom
mapObj = folium.Map(location=[21.437730075416685, 77.255859375],
                     zoom_start=7, tiles='openstreetmap')
# folium.TileLayer('stamenterrain', attr="stamenterrain").add_to(mapObj)

# create GeoJson layer to draw country borders
# style options - https://leafletjs.com/reference-1.7.1.html#path
bordersStyle = {"color": 'green', 'weight': 2, 'fillOpacity': 0}
bordersLayer = folium.GeoJson(
    data="states_india.geojson",
    name="Borders",
    style_function=lambda x: bordersStyle)
bordersLayer.add_to(mapObj)

# create a layer for bubble map using FeatureGroup
powerPlantsLayer = folium.FeatureGroup("Power Plants")
# add the created layer to the map
powerPlantsLayer.add_to(mapObj)

# iterate through each dataframe row
for i in range(len(dataDf)):
    areaStr = dataDf.iloc[i]['area']
    fuelStr = dataDf.iloc[i]['fuel']
    capVal = dataDf.iloc[i]['capacity']
    # derive the circle color
    clr = "blue" if fuelStr.lower() == 'wind' else "red"
    # derive the circle radius
    radius = capVal*100
    # derive the circle pop up html content 
    popUpStr = 'Area - {0}<br>Fuel - {1}<br>Capacity - {2} MW'.format(
        areaStr, fuelStr, capVal)
    # draw a circle for the power plant on the layer
    folium.Circle(
        location=[dataDf.iloc[i]['lat'], dataDf.iloc[i]['lng']],
        popup=folium.Popup(popUpStr, min_width=100, max_width=700),
        radius=radius,
        color=clr,
        weight=2,
        fill=True,
        fill_color=clr,
        fill_opacity=0.1
    ).add_to(powerPlantsLayer)


# add layer control over the map
folium.LayerControl().add_to(mapObj)

# html to be injected for displaying legend
legendHtml = '''
     <div style="position: fixed; 
     bottom: 50px; left: 50px; width: 150px; height: 70px; 
     border:2px solid grey; z-index:9999; font-size:14px;
     ">&nbsp; Fuel Types <br>
     &nbsp; <i class="fa fa-circle"
                  style="color:blue"></i> &nbsp; Wind<br>
     &nbsp; <i class="fa fa-circle"
                  style="color:red"></i> &nbsp; Solar<br>
      </div>
     '''

# inject html corresponding to the legend into the map
mapObj.get_root().html.add_child(folium.Element(legendHtml))

# save the map as html file
mapObj.save('output.html')
```



![bubble_map_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/bubble_map_demo.png)
### Video
The video for this post can be seen [here](https://youtu.be/lHuHrm8awbw)

<iframe width="560" height="315" src="https://www.youtube.com/embed/lHuHrm8awbw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### References
* Circle and GeoJson styling options - https://leafletjs.com/reference-1.7.1.html#path
* Folium Circle docs - https://python-visualization.github.io/folium/modules.html#folium.vector_layers.Circle
* Folium GeoJson docs - https://python-visualization.github.io/folium/modules.html#folium.features.GeoJson

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY4NzIxMjgxMywtMjA4ODc0NjYxMl19
-->