## Skill - Draw text on python folium maps using DivIcon

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Introduction to Folium for interactive maps in python](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html)
* [Inject HTML into python folium maps](https://nagasudhir.blogspot.com/2021/08/inject-html-into-python-folium-maps.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

 See [this](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html) post to learn about folium libary basics

<hr/>

* Text can be drawn on the map using markers. 
* While creating a marker, use ```DivIcon``` as the marker icon
* HTML can be used as the DivIcon content. So we can write the desired text in the DivIcon, to achieve the text-marker effect
* Since the content of a DivIcon is HTML, we can even style the text using injected CSS. Injecting CSS into folium maps can be seen [here](https://nagasudhir.blogspot.com/2021/08/inject-html-into-python-folium-maps.html) 

### Example
```python
# import folium library
import folium

mapObj = folium.Map(location=[24.2170111233401, 81.0791015625000],
                    zoom_start=5)

folium.Marker(location=[24.2170111233401, 81.0791015625000],
              popup=folium.Popup('<i>The center of map</i>'),
              tooltip='Center',
              icon=folium.DivIcon(html="""Hello World <b>ABCDEFG</b>""",
                                  class_name="mapText"),
              ).add_to(mapObj)

# inject html into the map html
mapObj.get_root().html.add_child(folium.Element("""
<style>
.mapText {
    white-space: nowrap;
    color:red;
    font-size:large
}
</style>
"""))

mapObj.save('output.html')
```

![folium_divicon_demo](https://raw.githubusercontent.com/nagasudhirpulla/taming_python/master/blog/skills/assets/img/folium_divicon_demo.PNG)
### Text that reacts to map zoom
* If we want to change the font size of the text based on the map zooming, we can create an event handler based on the map `zoomend` event to update the text font size based on the map zoom level.
* This behavior has to be injected as JavaScript in the output HTML file
* For attaching the event handler to the map object, the JavaScript variable name of map object is required. We can get the JavaScript map object variable
  
### Video
The video for this post can be found [here](https://youtu.be/yo58hzXeNBU)

<iframe width="560" height="315" src="https://www.youtube.com/embed/yo58hzXeNBU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI4MDA0NDMzLC02ODI5MzQ5ODYsLTEzMj
I3NDQxMDYsMTM1ODA0MjI1NCwtMjA0MzYyMTU2NSwtMTk0NjM5
ODg0NiwxNTc3MTgxMDI2LDEzNTE5MTY3MzMsMTI4NjI5NjUwMF
19
-->