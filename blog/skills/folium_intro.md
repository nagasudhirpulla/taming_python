## Skill - Intro to Interactive maps in python with Folium
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

In this post we will get a beginner level introduction to Folium library which is extensively **used for creating interactive maps** in python

### Installing folium
* Open command prompt and type ```python -m pip install folium```
![pip install folium](https://github.com/nagasudhirpulla/taming_python/raw/0aadac449b8f8e1b0a8659c79f32b3798aef991b/blog/skills/assets/img/folium_pip_install.png)
### Topics covered
* Initialize a folium map object with map center and zoom
* Set the tile layers from in-built sources
* Set the tile layers from other sources
* Layer controls button to show/hide layers
* Save a map object as html

### Initialize a folium map object with map center and zoom
Lets create a simple folium map object
```python
import folium

# the lists of x and y coordinates
x = [1, 2, 3, 4]
y = [1, 4, 2, 3]

# create a figure and axes handle using 'subplots' function
fig, ax = plt.subplots()

# use axes handle to plot xy data and get the plot artist in return
la, = ax.plot(x, y)

# set the title for our plot using axes handle
ax.set_title('Basic Matplotlib plot')

# set x and y axis titles using axes handle
ax.set_xlabel("X Data")
ax.set_ylabel("Y Data")

# set label to the plot for the sake of legend using the plot artist
la.set_label('basic_plot')

# enable legends for the axes handle
ax.legend()

# print the plot
plt.show()
```
![plot_python_output](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/basic_matplotlib_plot.png)
Congrats!, we just covered the intro, installation and very basic plotting skills of *Matplotlib*

I would also like to point out that in the [anatomy of figure](https://matplotlib.org/3.2.1/gallery/showcase/anatomy.html) page, the code with which the diagram is created is mentioned below it. That code is a very useful as a reference for beginners on how to create plots, titles, legends etc

### Video
You can the video on this post [here](https://youtu.be/Cy789_J-RWY)

<iframe width="560" height="315" src="https://www.youtube.com/embed/Cy789_J-RWY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/

### Basic Plot Example
<iframe src="https://trinket.io/embed/python3/b3c8e34720" width="100%" height="356" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

### References
* Examples gallery - https://matplotlib.org/gallery/index.html
* medium post - https://towardsdatascience.com/data-visualization-using-matplotlib-16f1aae5ce70
* anatomy of a figure - https://matplotlib.org/3.2.1/gallery/showcase/anatomy.html
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbODYwNzY3Mzk1LC0xODI3MzQxODY2XX0=
-->