## Skill - Export a Matplotlib figure as an image or a pdf file
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

In this post we will try to understand how to export a matplotlib figure as an image or pdf file

Please make sure that you covered the [post on basics](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)

<hr/>

### Using "savefig" method to save the figure as a file
```python
import matplotlib.pyplot as plt

# create a plotting area and get the figure, axes handle in return
fig, ax = plt.subplots()

# plot some data
ax.plot([0,4,8,12], [6,8,4,2])

# plot again
ax.plot([0,3,9,12,15,18], [2,1,9,6,4,3])

# print plot
plt.show()

# save figure as a png file
fig.savefig("output.png")
fig.savefig(r"C:\figure.jpg")
fig.savefig(r"C:\testFile.pdf")
```
![basic multiple plots output](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/basic_multiple_plots.png)
As shown in the above code, just by using the ```savefig``` method on a matplotlib figure, we can export the figure as a pdf or image

### More styled example
This example is the same as above, but adds some extra styling.
Please make sure you covered the [styling plots](https://nagasudhir.blogspot.com/2020/05/styling-matplotlib-plots.html) post in order to understand this code.
```python
import matplotlib.pyplot as plt

# create a plotting area and get the figure, axes handle in return
fig, ax = plt.subplots()

# set plot title
ax.set_title('Multiple plots example')

# set x and y labels
ax.set_xlabel('this is X-axis')
ax.set_ylabel('this is Y-axis')

# plot some data and get the line artist object in return
la1, = ax.plot([0,4,8,12], [6,8,4,2], color='#de689f')

# set label to line artist object for legend
la1.set_label('First Plot')

# plot again and get the line artist object in return
la2, = ax.plot([0,3,9,12,15,18], [2,1,9,6,4,3], color='#a155b9')

# set label to line artist object for legend
la2.set_label('Second Plot')

# set a marker style
la2.set_marker('o')

# enable legends
ax.legend()

# print plot
plt.show()
```
![styled basic multiple plots output](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/basic_multiple_plots_styled.png)
### Video
You can the video on this post [here](https://youtu.be/2AOZx14y8Xk)

<iframe width="560" height="315" src="https://www.youtube.com/embed/2AOZx14y8Xk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/ or https://repl.it/repls/MountainousWhirlwindRatios

### Multiple plots example
<iframe src="https://trinket.io/embed/python3/3bc5748621" width="100%" height="356" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

### Styled multiple plots example
<iframe src="https://trinket.io/embed/python3/93046401c2" width="100%" height="356" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

### References
*  plot function API - https://matplotlib.org/2.1.1/api/_as_gen/matplotlib.pyplot.plot.html
* Examples gallery - https://matplotlib.org/gallery/index.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAwOTY3NTk4Nl19
-->