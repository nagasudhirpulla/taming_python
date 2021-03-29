## Skill - Styling Matplotlib plots
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Introduction to Matplotlib plotting library](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

**Matplotlib** is a plotting library in the scipy ecosystem of libraries.

In this post we will try to understand how to control the styling of a Matplotlib plot

Please make sure that you covered the [post on basics](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)

### Color
use `color` parameter in plot function. color can be a known color like `'red'` string or a hex color like `'#0F0F0F'`. You can use online color pickers like [this](https://cssgenerator.org/rgba-and-hex-color-generator.html) to generate hex codes from colors.
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [1, 4, 2, 3]

# create a new figure and get figure, axes handle in return
fig, ax = plt.subplots()

# using color keyword in plot function to control color
ax.plot(x,y,color='magenta')

# print figure
plt.show()
```
![plot color demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_plot_color_demo.png)
### Line style
linestyle can be `'solid', 'dashed',  'dashdot', 'dotted', 'None'`
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [1, 4, 2, 3]

# create a new figure and get figure, axes handle in return
fig, ax = plt.subplots()

# using linestyle keyword in plot function
ax.plot(x,y,linestyle='dashed')

# print figure
plt.show()
```
![plot line style demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_plot_linestyle_demo.png)
### Markers
marker parameter can be used to control the marker style. For example, here we are using `marker='p'` to use pentagon marker. 
Marker strings like the one used above can be found [here](https://matplotlib.org/2.1.1/api/markers_api.html#module-matplotlib.markers)
Other marker styling options are
```
markeredgecolor / mec - control the color of marker edge / outline

markeredgewidth / mew - a number that can control the marker outline/edge width

markerfacecolor / mfc - control the color of marker filling inside the outline

markersize / ms - a number that can control the size of the marker
```
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [1, 4, 2, 3]

# create a new figure and get figure, axes handle in return
fig, ax = plt.subplots()

# using marker, ms, mfc, mec, mew keywords in plot function to control marker appearance
ax.plot(x,y,marker='p', ms=15, mfc='magenta', mec='yellow', mew=3)

# print figure
plt.show()
```
![plot marker demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_plot_marker_demo.png)
### Styling plots using format string
the `plot` function accepts a format string as the 3rd input for specifying the line style in a single string.
```ax.plot([<x_vals>], [<y_vals>], <fmt>)```

`fmt` string should in the format ```'[marker][line][color]'```
![matplotlib line style formats](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_line_style_formats.PNG)
Example formats are shown below
```python
'b'    # blue markers with default shape
'or'   # red circles
'-g'   # green solid line
'--'   # dashed line with default color
'^k:'  # black triangle_up markers connected by a dotted line
```

An example of styling a plot using format string can be seen below
```python
import matplotlib.pyplot as plt

# the lists of x and y coordinates
x = [1, 2, 3, 4]
y = [1, 4, 2, 3]

# create a figure and axes handle using 'subplots' function
fig, ax = plt.subplots()

# use axes handle to plot xy data and get the plot artist in return
la, = ax.plot(x, y, '*-r')
# In the format string, * means marker style, - means normal line, r means red color

# print the plot
plt.show()
```
![plot with format string](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/basic_matplotlib_plot_with_line_format_string.png)
For more styling options an in depth understanding of styling please check out the [api documentation page](https://matplotlib.org/2.1.1/api/_as_gen/matplotlib.pyplot.plot.html)

### Video
You can the video on this post [here](https://youtu.be/CijoqFJGRu0)

<iframe width="560" height="315" src="https://www.youtube.com/embed/CijoqFJGRu0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/ or https://repl.it/repls/MountainousWhirlwindRatios

### Color example
<iframe src="https://trinket.io/embed/python3/026c5476b1" width="100%" height="356" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

### Line style example
<iframe src="https://trinket.io/embed/python3/28a9eb549a" width="100%" height="356" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>


### Markers example
<iframe src="https://trinket.io/embed/python3/77771190ab" width="100%" height="356" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

### Format string example
<iframe src="https://trinket.io/embed/python3/09f1cdf07b" width="100%" height="356" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

### References
* plot function API - https://matplotlib.org/2.1.1/api/_as_gen/matplotlib.pyplot.plot.html
* matplotlib colors - https://matplotlib.org/2.1.1/api/colors_api.html
* Examples gallery - https://matplotlib.org/gallery/index.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFN0eWxpbmcgTWF0cGxvdG
xpYiBQbG90c1xuYXV0aG9yOiBOYWdhc3VkaGlyIFB1bGxhXG5k
YXRlOiAnMjAyMC0wNS0wOCdcbnRhZ3M6ICdweXRob24sIGxlYX
JuaW5nLCB0dXRvcmlhbCwgdGFtaW5nX3B5dGhvbl9za2lsbCdc
bmNhdGVnb3JpZXM6IHRhbWluZ19weXRob25fc2tpbGxcbiIsIm
hpc3RvcnkiOlstMTI0MzExODYxLDQ4NjkxNzI2Myw5MzQ1MjE4
MTIsNDg2OTE3MjYzLDU3NjY5Mjg5NCwtMzI4ODU3MTA5LDMyMT
QwMDYxMCwtMTM4MDA1MzcxMSwtMTg2Mzg2MjEyNl19
-->