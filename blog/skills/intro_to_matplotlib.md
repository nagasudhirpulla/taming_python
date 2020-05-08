## Skill - Intro to Matplotlib
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>
In this post we will get a beginner level introduction to Matplotlib library which is extensively used for plotting in python

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

# create a figure with axes
fig, ax = plt.subplots()

# plot data on the axes
ax.plot(x, y)

# set the title for our plot
ax.set_title('Basic Matplotlib plot')

# set x and y axis titles
ax.set_xlabel("X Data")
ax.set_ylabel("Y Data")

# set label to the plot for the sake of legend
ax.set_label('basic_plot')

# enable legends for the axes
ax.legend()

# print the plot
plt.show()
```

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/ or https://repl.it/repls/MountainousWhirlwindRatios

### References
* Examples gallery - https://matplotlib.org/gallery/index.html
* medium post - https://towardsdatascience.com/data-visualization-using-matplotlib-16f1aae5ce70
* anatomy of a figure - https://matplotlib.org/3.2.1/gallery/showcase/anatomy.html
<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjM3ODI1ODEzLDE0NjY5MDU1OTAsMTk3NT
g3Njk2NCwtMTA5MDAyMzk5MCwtMjc4NTQ0MDM1LC0yMDU1MzA1
NjQ1LC0xODIzNDE2NzU1LDUxMDUwOTc2OSwxMjIyODYwMjkwXX
0=
-->