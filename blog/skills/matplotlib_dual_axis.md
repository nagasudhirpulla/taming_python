## Secondary axis and twin axis in python matplotlib plots
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Introduction to Matplotlib plotting library](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)
* [Styling Matplotlib plots](https://nagasudhir.blogspot.com/2020/05/styling-matplotlib-plots.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

**Matplotlib** is a plotting library tn the scipy ecosystem of libraries.

Please make sure that you covered the [post on basics](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)
<hr/>

Sometimes we may require to have the main axis lines to be intersecting at (0,0) of the subplot. We will control the positioning of `spines` to achieve this.

```python
import matplotlib.pyplot as plt
x = [-5, -4, 5, 8]
y = [-6, 5, 8,-10]

# create a plotting area and get the figure, axes handle in return
fig, ax = plt.subplots()

# plot data on the axes handle
ax.plot(x, y)

# Move left y-axis and bottim x-axis to centre by setting position as 'center'
ax.spines['left'].set_position('zero')
ax.spines['bottom'].set_position('zero')

# Eliminate top and right axes by setting spline color as 'none'
ax.spines['right'].set_color('none')
ax.spines['top'].set_color('none')

# print the plot
plt.show()
```

![matplotlib_center_axes_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_center_axes_0_0_demo.PNG)

As shown above the spines/axis lines of an axes handle `ax` can be controlled by `ax.spines`

If we want the axis lines to be intersecting at center of the subplot instead of (0,0). 

In such case we can use the following 
```python
ax.spines['left'].set_position('center')
ax.spines['bottom'].set_position('center')
```
The output would be like the image below
![matplotlib_center_axes_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_center_axes_demo.PNG)

### Video
You can the video on this post [here](https://youtu.be/qzFOFP1hxvg)

<iframe width="560" height="315" src="https://www.youtube.com/embed/qzFOFP1hxvg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/

### References
* Solution from stackoverflow post - https://stackoverflow.com/questions/31556446/how-to-draw-axis-in-the-middle-of-the-figure
* Spine placement demo - https://matplotlib.org/3.1.0/gallery/ticks_and_spines/spine_placement_demo.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwODcwMTc5MjddfQ==
-->