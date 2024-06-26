## Skill - Set axes ticks and tick labels in matplotlib
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

Please make sure that you covered the[post on basics](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)
<hr/>

Sometimes we may desire to control the location of axis ticks of our subplots. This can be achieved by using the `set_xticks` and `set_yticks` functions of the axes handle.

### Example - specify the position of axis ticks using `set_xticks` and `set_yticks`
```python
import matplotlib.pyplot as plt
x = [0,1,2,3,4,5,6,7,8]
y = [8,6,4,2,9,7,6,3,1]

# create a plotting area and get the figure, axes handle in return
fig, ax = plt.subplots()

# plot data on the axes handle
ax.plot(x, y)

# specify the position of x axis ticks
ax.set_xticks([0,2,4,6,8])

# specify the position of y axis ticks
ax.set_yticks([0,3,6,9])

# print the plot
plt.show()
```
![matlpotlib_axis_ticks_demo**](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matlpotlib_axis_ticks_demo.png)

In order to use custom tick labels instead of default tick labels, we can use `set_xticklabels` and `set_yticklabels` functions of the axes handle

### Example - specify the axis labels using `set_xticklabels` and `set_yticklabels`
```python
import matplotlib.pyplot as plt
x = [0,1,2,3,4,5,6,7,8]
y = [8,6,4,2,9,7,6,3,1]

# create a plotting area and get the figure, axes handle in return
fig, ax = plt.subplots()

# plot data on the axes handle
ax.plot(x, y)

# specify the position of x axis ticks
ax.set_xticks([0,2,4,6,8])

# specify the tick labels of x axis
ax.set_xticklabels(['zero','two','four','six','eight'])

# specify the position of y axis ticks
ax.set_yticks([0,3,6,9])

# print the plot
plt.show()
```
![matlpotlib_axis_tick_labels_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matlpotlib_axis_tick_labels_demo.png)

### Example - avoid axis ticks by specifying empty array
```python
import matplotlib.pyplot as plt
x = [0,1,2,3,4,5,6,7,8]
y = [8,6,4,2,9,7,6,3,1]

# create a plotting area and get the figure, axes handle in return
fig, ax = plt.subplots()

# plot data on the axes handle
ax.plot(x, y)

# provide empty array to specify that x axis ticks not required
ax.set_xticks([])

# print the plot
plt.show()
```

![matlpotlib_blank_axis_tick_labels_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matlpotlib_blank_axis_tick_labels_demo.png)
### Video
You can the video on this post [here](https://youtu.be/qaUrn5sdEH0)

<iframe width="560" height="315" src="https://www.youtube.com/embed/qaUrn5sdEH0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/

### References
* official documentation on set axis ticks - https://matplotlib.org/3.2.1/api/_as_gen/matplotlib.axes.Axes.set_xticks.html#matplotlib.axes.Axes.set_xticks
* another post - https://www.tutorialspoint.com/matplotlib/matplotlib_setting_ticks_and_tick_labels.htm
* another post - https://jakevdp.github.io/PythonDataScienceHandbook/04.10-customizing-ticks.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFNldCBheGVzIHRpY2sgbG
FiZWxzIGluIG1hdHBsb3RsaWJcbmF1dGhvcjogTmFnYXN1ZGhp
ciBQdWxsYVxudGFnczogJ3B5dGhvbiwgbGVhcm5pbmcsIHR1dG
9yaWFsLCB0YW1pbmdfcHl0aG9uX3NraWxsJ1xuY2F0ZWdvcmll
czogdGFtaW5nX3B5dGhvbl9za2lsbFxuZGF0ZTogJzIwMjAtMD
UtMTUnXG4iLCJoaXN0b3J5IjpbMTYxNDk1MjUwNCwzODUxNjE0
NjYsNzEwNjI2NzEsMTc0ODMyMTE3OSwxNjc2MjY3ODk2LC00OT
AwMzcxOTFdfQ==
-->