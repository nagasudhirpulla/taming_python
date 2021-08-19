## Skill - Inject HTML into python folium maps

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Introduction to Folium for interactive maps in python](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will learn how to inject HTML into a folium map in python

 See [this](https://nagasudhir.blogspot.com/2021/07/introduction-to-folium-for-interactive.html) post to learn about folium libary basics

### Example
In this example code below, we are injecting a ```div``` element into the HTML body output map.
```python
# import folium library
import folium

# create a map object with initial zoom and map center
mapObj = folium.Map(location=[20.658486188041294, 82.65014648437501], zoom_start=7)

# inject html into the map html
mapObj.get_root().html.add_child(folium.Element("""
<div style="position: fixed; 
     top: 50px; left: 70px; width: 150px; height: 70px; 
     background-color:orange; border:2px solid grey;z-index: 900;">
    <h5>Hello World!!!</h5>
    <button>Test Button</button>
</div>
"""))

mapObj.save('output.html')
```

![folium_inject_html_demo](https://raw.githubusercontent.com/nagasudhirpulla/taming_python/master/blog/skills/assets/img/folium_inject_html_demo.PNG)

### Points to remember
* Similar to the above example, we can also inject CSS by injecting the ```style``` tag into the HTML body of the map. 
* Set the ```z-index``` CSS attribute of the injected HTML elements to a higher value. Otherwise, the injected HTML elements will be hidden behind the map.

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5Mjk0MzYzMDMsMTY2MzU2Nzc5MywxOD
YwMjMzMTE2LDgyNTU5Nzc2OCwxNzQ2MjMyNTcwXX0=
-->