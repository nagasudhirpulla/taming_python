## Skill - Control axis ticks locations using tick locators in matplotlib
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

Sometimes we may desire to control the location of axis ticks of our subplots. This can be achieved by using the TickLocators

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
![matlpotlib_axis_ticks_demo](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/matlpotlib_axis_ticks_demo.png)

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

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/ or https://repl.it/repls/MountainousWhirlwindRatios

### You can practice here


### References
* 

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IENvbnRyb2xsaW5nIHRpY2
sgbG9jYXRpb25zIHVzaW5nIE1hdHBsb3RsaWIgVGlja0xvY2F0
b3JcbmF1dGhvcjogTmFnYXN1ZGhpciBQdWxsYVxudGFnczogJ3
B5dGhvbiwgbGVhcm5pbmcsIHR1dG9yaWFsLCB0YW1pbmdfcHl0
aG9uX3NraWxsJ1xuY2F0ZWdvcmllczogdGFtaW5nX3B5dGhvbl
9za2lsbFxuZGF0ZTogJzIwMjAtMDUtMTcnXG4iLCJoaXN0b3J5
IjpbMTY2OTg1NDE3MCwxMzYxMDg4NzQwXX0=
-->