## Skill - Setting the Figure size of Matplotlib plots
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

In this post we will try to learn how to set the size of a figure in matplotlib

Please make sure that you covered the [post on basics](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)
<hr/>

Sometimes we may like to control the size of matplotlib figure instead of default figure size. This requirement may arise for saving figure as image etc

### Setting figure size using the 'figsize' parameter
Here we can see that  are providing `figsize` input to `subplots` function as tuple in the form `figsize=(width_inches, height_inches)`
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [1, 4, 2, 3]

# create a new figure and get figure, axes handle in return
fig, ax = plt.subplots(figsize=(8,8))

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

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/ or https://repl.it/repls/MountainousWhirlwindRatios

### Color example


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
hpc3RvcnkiOlsxODgzNTAwNjMyLDQ4NjkxNzI2Myw1NzY2OTI4
OTQsLTMyODg1NzEwOSwzMjE0MDA2MTAsLTEzODAwNTM3MTEsLT
E4NjM4NjIxMjZdfQ==
-->