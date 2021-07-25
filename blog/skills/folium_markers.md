## Skill - Draw markers in python folium maps

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Introduction to Folium for interactive maps in python](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will learn how to draw markers on a folium map in python

 See [this](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html) post to learn about folium libary basics

### Create a simple marker
* You can create a marker on a folium map using ```folium.Marker``` function. 
* You can specify the marker location using the ```location``` input of the function
```python
# import folium library
import folium

# create a map object
mapObj = folium.Map(location=[24.2170111233401, 81.0791015625000],
                    zoom_start=5)

# add a marker object to the map
folium.Marker(location=[24.2170111233401, 81.0791015625000]
              ).add_to(mapObj)

# save the map to a html file
mapObj.save('output.html')
```

### Adding a Pop up content and tool-tip text to a marker
* Use the ```popup``` input of ```folium.Marker``` function add pop-up HTML content
* Use the ```tooltip``` input of ```folium.Marker``` function add tool-tip text
```python
folium.Marker(location=[24.2170111233401, 81.0791015625000],
              popup=folium.Popup('<i>The center of map</i>'),
              tooltip='Some Text'
              ).add_to(mapObj)
```

### Change icon of the marker with fontawesome and bootstrap markers
Use the ```icon``` input of ```folium.Marker``` function to change icon of the marker

For using glyphicons by bootstrap specify the icon name from [here](https://getbootstrap.com/docs/3.3/components/)
```python
folium.Marker(location=[20, 79],
              icon=folium.Icon(icon='glyphicon-plane', color='green')
              ).add_to(mapObj)
```

if you prefer to use selenium with chrome, download Chrome WebDriver from https://sites.google.com/a/chromium.org/chromedriver/downloads

<hr/>

### References
* GeckoDriver for firefox - https://github.com/mozilla/geckodriver/releases
* Selenium Docs - https://selenium-python.readthedocs.io/getting-started.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbNjIyMTQ2MTc2LC0xMjk4MDg5MDAyLC0xMj
gwMzkxMjE5XX0=
-->