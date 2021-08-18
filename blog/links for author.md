python notes -  http://thomas-cokelaer.info/tutorials/python/basics.html#the-basics

matplotlib overview tutorial - https://towardsdatascience.com/data-visualization-using-matplotlib-16f1aae5ce70


### TODOS
* bubble map geographic plots using folium 
```python
"""
folium quickstart - https://python-visualization.github.io/folium/quickstart.html
folium docs - http://python-visualization.github.io/folium/modules.html#
circle options reference - https://leafletjs.com/reference-1.6.0.html#circle
leaflet js - https://leafletjs.com/index.html
"""

import pandas as pd
import folium

# read data as dataframe
dataDf = pd.read_excel('down_streams_info.xlsx')

# initialize a map with center and zoom
mapObj = folium.Map(location=[21.437730075416685, 77.255859375],
                     zoom_start=7, tiles='openstreetmap')
# folium.TileLayer('stamenterrain', attr="stamenterrain").add_to(mapObj)

# show borders
# style options - https://leafletjs.com/reference-1.7.1.html#path
bordersStyle = {"fillColor": 'green',
                'color': 'green', 'weight': 2, 'fillOpacity': 0}
bordersLayer = folium.GeoJson(
    data=(open("states_india.geojson", 'r').read()),
    name="Borders",
    style_function=lambda x: bordersStyle)
bordersLayer.add_to(mapObj)

powerPlantsLayer = folium.FeatureGroup("Power Plants")
# iterate through each dataframe row
for i in range(len(dataDf)):
    areaStr = dataDf.iloc[i]['area']
    fuelStr = dataDf.iloc[i]['fuel']
    capStr = dataDf.iloc[i]['capacity']
    clr = "blue" if fuelStr.lower() == 'wind' else "red"
    radius = capStr*100
    popUpStr = 'Area - {0}<br>Fuel - {1}<br>Capacity - {2} MW'.format(
        areaStr, fuelStr, capStr)
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

powerPlantsLayer.add_to(mapObj)

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

# inject html into the map html
mapObj.get_root().html.add_child(folium.Element(legendHtml))

# save the map as html file
mapObj.save('wind_locations.html')
```

* Histogram in python
* Manage application configuration or application secrets in Excel  
* global variables and using them inside functions- https://instructobit.com/tutorial/108/How-to-share-global-variables-between-files-in-Python
* python subprocess communication - https://eli.thegreenplace.net/2017/interacting-with-a-long-running-child-process-in-python/
* rounding of decimals while printing and rounding the number itself
* flask server basics
* naming conventions for classes (nouns), variables (nouns), functions (verbs), using camel case, avoid obvious names and use contextual names for better readability



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNzkxNjA5NDQsOTkwNTEzMTExLC04OD
ExMzgzODEsLTk4OTQ3NzI2MSwtMjA1NjQwNTU1MCwtOTc4Njcz
NDEsLTMyMzk4ODE0OSwtMTkyMzc2Mzk0NywzOTQ1Mzc4NjksLT
EzOTE0OTU2MDUsLTIyMTg4OTk3NSw2NjE2NzQwMTQsOTI2Nzk1
MzA0LC0zOTg1NDI2MDAsMTE3MjIzNjI4MywxODUyMDA2MDI1LD
IxMjE1NzcxNCwtNzc0ODYwMTQzLC01MjA0NzE5MzgsNzM5MDcz
Nzc5XX0=
-->