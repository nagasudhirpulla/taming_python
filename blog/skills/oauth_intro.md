## Skill - OAuth 2.0 for centralized Authorization and Authentication of users and applications
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

Sometimes we may desire to control the location of axis ticks of our subplots. This can be achieved by using `TickLocators` in matplotlib.

TickLocators help matplotlib to determine the location of ticks

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
| Locator class     | Description                                             |
|-------------------|---------------------------------------------------------|
| NullLocator       | No ticks                                                |
| FixedLocator      | Tick locations are fixed                                |
| IndexLocator      | Locator for index plots (e.g., where x = range(len(y))) |
| LinearLocator     | Evenly spaced ticks from min to max                     |
| LogLocator        | Logarithmically ticks from min to max                   |
| MultipleLocator   | Ticks and range are a multiple of base                  |
| MaxNLocator       | Finds up to a max number of ticks at nice locations     |
| AutoLocator       | (Default.) MaxNLocator with simple defaults.            |
| AutoMinorLocator  | Locator for minor ticks                                 |

![tick_locators_illustration](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/tick_locators_illustration.png)
Check out [this post](https://matplotlib.org/3.1.1/gallery/ticks_and_spines/tick-locators.html) for all locators example code

### Video
You can the video on this post [here](https://youtu.be/oazc83ZZgpg)

<iframe width="560" height="315" src="https://www.youtube.com/embed/oazc83ZZgpg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/

### References
* Official guide - https://matplotlib.org/3.1.1/gallery/ticks_and_spines/tick-locators.html
* Official documentation - https://matplotlib.org/3.1.1/api/ticker_api.html#tick-locating
* another post - https://jakevdp.github.io/PythonDataScienceHandbook/04.10-customizing-ticks.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIzMTY2NjAxMl19
-->