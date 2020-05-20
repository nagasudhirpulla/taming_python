## Skill - format axis ticks using TickFormatters in matplotlib
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

Sometimes we want to explicitly control the formatting of ticks like number of decimal places, date formats etc. This can be done through `TickFormatters`

### Control spacing between ticks using 'MultipleLocator'
```python
import matplotlib.pyplot as plt
x = [0,1,2,3,4,5,6,7,8]
y = [8,6,4,2,9,7,6,3,1]

# create a plotting area and get the figure, axes handle in return
fig, ax = plt.subplots()

# plot data on the axes handle
ax.plot(x, y)

# set x axis major ticks for multiples of 3 like 0,3,6,9 etc
ax.xaxis.set_major_locator(plt.MultipleLocator(3))

# set x axis minor ticks for multiples of 1 like 0,1,2,3,4 etc
ax.xaxis.set_minor_locator(plt.MultipleLocator(1))

# print the plot
plt.show()
```
![matplotlib_multiplelocator_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_multiplelocator_demo.PNG)

### Fixing the number of ticks on the axis using 'LinearLocator'
```python
import matplotlib.pyplot as plt
x = [0,1,2,3,4,5,6,7,8]
y = [8,6,4,2,9,7,6,3,1]

# create a plotting area and get the figure, axes handle in return
fig, ax = plt.subplots()

# plot data on the axes handle
ax.plot(x, y)

# set number of minor ticks on the axis as 16
ax.xaxis.set_minor_locator(plt.LinearLocator(numticks=16))
# set number of major ticks on the axis as 6
ax.xaxis.set_major_locator(plt.LinearLocator(numticks=6))

# print the plot
plt.show()
```
![matplotlib_linearlocator_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_linearlocator_demo.PNG)

### Using 'LogLocator' for logarithmic scaling of axis
```python
import matplotlib.pyplot as plt
x = [0,20,300,50000,600000,7000000]
y = [8,7,6,3,5,9]

# create a plotting area and get the figure, axes handle in return
fig, ax = plt.subplots()

# plot data on the axes handle
ax.plot(x, y)

# make axis scale as 'log'
ax.set_xscale('log')
# use log locator of major and minor x axis ticks
ax.xaxis.set_major_locator(plt.LogLocator(base = 10.0))

# print the plot
plt.show()
```
![matplotlib_loglocator_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_loglocator_demo.PNG)

### Hiding ticks using 'NullLocator'
```python
import matplotlib.pyplot as plt
x = [0,1,2,3,4,5,6,7,8]
y = [8,6,4,2,9,7,6,3,1]

# create a plotting area and get the figure, axes handle in return
fig, ax = plt.subplots()

# plot data on the axes handle
ax.plot(x, y)

# use null locator to hide major and minor ticks
ax.yaxis.set_major_locator(plt.NullLocator())
ax.yaxis.set_minor_locator(plt.NullLocator())
ax.xaxis.set_minor_locator(plt.NullLocator())
ax.xaxis.set_major_locator(plt.NullLocator())

# print the plot
plt.show()
```
![matplotlib_nulllocator_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_nulllocator_demo.PNG)

### Summary of Locators
| FormatterClass     | Description                             |
|--------------------|-----------------------------------------|
| NullFormatter      | No labels on the ticks                  |
| IndexFormatter     | Set the strings from a list of labels   |
| FixedFormatter     | Set the strings manually for the labels |
| FuncFormatter      | User-defined function sets the labels   |
| FormatStrFormatter | Use a format string for each value      |
| ScalarFormatter    | (Default.) Formatter for scalar values  |
| LogFormatter       | Default formatter for log axes          |

![tick_locators_illustration](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/tick_locators_illustration.png)
Check out [this post](https://matplotlib.org/3.1.1/gallery/ticks_and_spines/tick-locators.html) for all locators example code

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/ or https://repl.it/repls/MountainousWhirlwindRatios

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/GrossCreativeApplicationprogrammer?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### References
* Official guide - https://matplotlib.org/3.2.1/gallery/ticks_and_spines/tick-formatters.html
* Official documentation - https://matplotlib.org/3.1.1/api/ticker_api.html#tick-formatting
* another post - https://jakevdp.github.io/PythonDataScienceHandbook/04.10-customizing-ticks.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)





https://jakevdp.github.io/PythonDataScienceHandbook/04.10-customizing-ticks.html

https://stackoverflow.com/questions/29188757/matplotlib-specify-format-of-floats-for-tick-labels/29188910#29188910


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IEZvcm1hdCBheGlzIHRpY2
tzIGluIG1hdHBsb3RsaWJcbmF1dGhvcjogTmFnYXN1ZGhpciBQ
dWxsYVxuZGF0ZTogJzIwMjAtMDUtMTYnXG50YWdzOiAncHl0aG
9uLCBsZWFybmluZywgdHV0b3JpYWwsIHRhbWluZ19weXRob25f
c2tpbGwnXG5jYXRlZ29yaWVzOiB0YW1pbmdfcHl0aG9uX3NraW
xsXG4iLCJoaXN0b3J5IjpbMjA1MTc5NzU4LC05MjQzOTI5MTUs
MTY5MjQyMzU1NSw0NDYxOTAzODksMjA1ODc4NjUwOV19
-->