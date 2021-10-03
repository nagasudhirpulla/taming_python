## Skill - Place the legend at the bottom of a matplotlib plot
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Introduction to Matplotlib plotting library](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

**Matplotlib** is a plotting library tn the scipy ecosystem of libraries.

Please make sure that you covered the [post on basics](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)
<hr/>

Sometimes we might want to place the legend at the bottom of a matplotlib plot. This can be achieved using the ```bbox_to_anchor``` and ```loc="upper center"``` inputs of the ```legend``` function.

```python
import matplotlib.pyplot as plt
import random

# create figure and axes
fig, ax = plt.subplots(figsize=(11, 6))

# set plot title ans axis labels
ax.set_title("Bottom Legend Example")
ax.set_xlabel("X axis values")
ax.set_ylabel("Random numbers")

# x axis values
xVals = [x for x in range(20)]

for pltItr in range(5):
    # create random y axis values
    yVals = [random.randint(50, 100) for x in xVals]
    # create a line plot with x and y values
    la, = ax.plot(xVals, yVals)
    # set plot label for legend
    la.set_label("Trace {0}".format(pltItr+1))

# enable legend with bottom positioning
ax.legend(loc='upper center', bbox_to_anchor=(0.5, -0.1),
          shadow=True, ncol=5)

# adjust layout elements along with adding outer padding as 1 inch
fig.tight_layout(pad=1)

# save the figure as a png file
fig.savefig("output.png")
```

![matplotlib_center_axes_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_legend_bottom_demo.png)

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
eyJoaXN0b3J5IjpbLTI0ODMzMDcwNiwtMzUwMjg2NzU4LC0yND
UxNzQ2NTMsMTA2NTU3ODY3MywtMTQ4NjgzMTU4XX0=
-->