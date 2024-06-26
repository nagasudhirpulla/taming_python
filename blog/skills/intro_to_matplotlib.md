## Skill - Intro to Matplotlib
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>
In this post we will get a beginner level introduction to Matplotlib library which is extensively **used for plotting** in python

**Matplotlib** is a plotting library in the scipy ecosystem of libraries.

### Installing Matplotlib
* Open command prompt and type ```pip install matplotlib```
![pip install matplotlib](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/install_matplotlib.png)
### Anatomy of a matplotlib figure
* A graph in matplotlib is called a **figure**. It is like a canvas on which we draw figures.
* A matplotlib figure can have **plot, axis, title, legend, grid, ticks, tick labels, spines**
* The figure below describes all the components of a matplotlib figure. 
* Please take your time to understand the **terminology** used in matplotlib figure, since these terms will be used in matplotlib functions to **control the appearance of a figure**.
* You can refer to this figure any time to recollect the terminology used in matplotlib functions

![anatomy of a matplotlib figure](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/anatomy_of_matplotlib_figure.PNG)
* As shown above, in order to create a plot with matplotlib, we need to create a figure with axes

### Creating a basic line plot with lists of x and y coordinates
Lets create a simple line plot with x and y lists
```python
import matplotlib.pyplot as plt

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
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEludHJvIHRvIE1hdHBsb3
RsaWJcbmF1dGhvcjogTmFnYXN1ZGhpciBQdWxsYVxuZGF0ZTog
JzIwMjAtMDUtMDgnXG50YWdzOiAncHl0aG9uLCBsZWFybmluZy
wgdHV0b3JpYWwsIHRhbWluZ19weXRob25fc2tpbGwnXG5jYXRl
Z29yaWVzOiB0YW1pbmdfcHl0aG9uX3NraWxsXG4iLCJoaXN0b3
J5IjpbMTk0NTQzOTg5LDk3MDA3MzMzMSw1OTU5NzUyODcsLTIx
MTQ4NDc1MjMsMzI0MzM4ODM4LC0xNzEyNjA0NDIsMTIyMDY5Mz
YyNywyMTQ0MzE0OTc2LC03MTMzODQxMTcsNzY1MTQ2MDg3LDMz
MjI4NzQ0NSwxNDY2OTA1NTkwLDE5NzU4NzY5NjQsLTEwOTAwMj
M5OTAsLTI3ODU0NDAzNSwtMjA1NTMwNTY0NSwtMTgyMzQxNjc1
NSw1MTA1MDk3NjksMTIyMjg2MDI5MF19
-->