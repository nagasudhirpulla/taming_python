## Skill - Format axis ticks using TickFormatters in matplotlib
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

### Control axis tick labels with format string using 'StrMethodFormatter'
```python
import matplotlib.pyplot as plt
import matplotlib as mpl
x = [0,1,2,3,4,5,6,7,8]
y = [8,6,4,2,9,7,6,3,1]

# create a plotting area and get the figure, axes handle in return
fig, ax = plt.subplots()

# plot data on the axes handle
ax.plot(x, y)

# set x axis major ticks format as 2 decimal places
ax.xaxis.set_major_formatter(mpl.ticker.StrMethodFormatter('{x:0.2f}'))

# print the plot
plt.show()
```
![matplotlib_strmethod_formatter_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_strmethod_formatter_demo.PNG)
### Control axis tick labels text with user defined function using 'FuncFormatter'
`FuncFormatter` should be supplied with a **function** that takes in tick value and tick position and outputs the tick label string
```python
import matplotlib.pyplot as plt

x = [0,10000,20000,30000,40000,50000,60000,70000,80000]
y = [8,6,4,2,9,7,6,3,1]

# define the formatter function
# first input is the tick value, second input is the tick position
# returns the tick label string
def thousandsFormatter(x,pos):
	return '{0:.0f}K'.format(x/10000)

# create a plotting area and get the figure, axes handle in return
fig, ax = plt.subplots()

# plot data on the axes handle
ax.plot(x, y)

# set x axis major ticks format as 2 decimal places
ax.xaxis.set_major_formatter(plt.FuncFormatter(thousandsFormatter))

# print the plot
plt.show()
```
![matplotlib_func_formatter_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_func_formatter_demo.PNG)

### Setting axis tick labels manually using 'FixedFormatter'
`FixedFormatter` should be generally used along with `FixedLocator`. Otherwise the labels and ticks may not match most of the times.
```python
import matplotlib.pyplot as plt
x = [0,1,2,3,4,5,6,7,8]
y = [8,6,4,2,9,7,6,3,1]

# create a plotting area and get the figure, axes handle in return
fig, ax = plt.subplots()

# plot data on the axes handle
ax.plot(x, y)

# set number of major x tick locations manually using FixedLocator
ax.xaxis.set_major_locator(plt.FixedLocator(x))

# set x axis ticks labels manually using FixedFormatter
labels = ['zero','one','two','three','four','five','six','seven','eight']
ax.xaxis.set_major_formatter(plt.FixedFormatter(labels))

# print the plot
plt.show()
```
![matplotlib_linearlocator_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_fixed_formatter_demo.PNG)
### Hiding tick labels using 'NullFormatter'
```python
import matplotlib.pyplot as plt
x = [0,1,2,3,4,5,6,7,8]
y = [8,6,4,2,9,7,6,3,1]

# create a plotting area and get the figure, axes handle in return
fig, ax = plt.subplots()

# plot data on the axes handle
ax.plot(x, y)

# use null locator to hide major and minor ticks
ax.yaxis.set_major_formatter(plt.NullFormatter())
ax.yaxis.set_minor_formatter(plt.NullFormatter())
ax.xaxis.set_minor_formatter(plt.NullFormatter())
ax.xaxis.set_major_formatter(plt.NullFormatter())

# print the plot
plt.show()
```
![matplotlib_null_formatter_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_null_formatter_demo.PNG)
### 'DateFormatter' for formatting date labels
```python
import datetime as dt
import matplotlib.pyplot as plt
import matplotlib.dates as mdates

# get today date
today = dt.datetime.today()
numDays = 9

x = [today-dt.timedelta(days=p) for p in range(numDays)]
y = [8,6,4,2,9,7,6,3,1]

# create a plotting area and get the figure, axes handle in return
fig, ax = plt.subplots()

# set x axis major ticks date format using funcFormatter
ax.xaxis.set_major_formatter(plt.FuncFormatter(mdates.DateFormatter('%d-%b')))

# plot data on the axes handle
ax.plot(x, y)

# print the plot
plt.show()
```
![matplotlib_date_formatter_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_date_formatter_demo.PNG)

### Summary of Locators
| FormatterClass     | Description                             |
|--------------------|-----------------------------------------|
| NullFormatter      | No labels on the ticks                  |
| IndexFormatter     | Set the strings from a list of labels   |
| FixedFormatter     | Set the strings manually for the labels |
| FuncFormatter      | User-defined function sets the labels   |
| FormatStrFormatter | Use an old-style sprintf format string      |
| StrMethodFormatter | Use string [`format`](https://docs.python.org/3/library/functions.html#format "(in Python v3.8)") method      |
| ScalarFormatter    | Default formatter for scalars: autopick the format string  |
| LogFormatter       | Default formatter for log axes          |
| PercentFormatter       | Format labels as a percentage          |

![matplotlib_tick_formatters_illustration](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_tick_formatters_illustration.png)

Check out [this post](https://matplotlib.org/3.2.1/gallery/ticks_and_spines/tick-formatters.html) for all locators example code

### Video
You can the video on this post [here](https://youtu.be/QYBAP0YxSZU)

<iframe width="560" height="315" src="https://www.youtube.com/embed/QYBAP0YxSZU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/

### References
* Official guide - https://matplotlib.org/3.2.1/gallery/ticks_and_spines/tick-formatters.html
* Official documentation - https://matplotlib.org/3.1.1/api/ticker_api.html#tick-formatting
* another post - https://jakevdp.github.io/PythonDataScienceHandbook/04.10-customizing-ticks.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IGZvcm1hdCBheGlzIHRpY2
tzIHVzaW5nIFRpY2tGb3JtYXR0ZXJzIGluIG1hdHBsb3RsaWJc
bmF1dGhvcjogTmFnYXN1ZGhpciBQdWxsYVxuZGF0ZTogJzIwMj
AtMDUtMTYnXG50YWdzOiAncHl0aG9uLCBsZWFybmluZywgdHV0
b3JpYWwsIHRhbWluZ19weXRob25fc2tpbGwnXG5jYXRlZ29yaW
VzOiB0YW1pbmdfcHl0aG9uX3NraWxsXG4iLCJoaXN0b3J5Ijpb
MTA0ODIzNjIwNywtNjEyNjk2MDE5LDkyNTczNzkzNywtMTk1Nz
M2NDYsNDY0ODQ2OTQ4LC0xMDA3NjkyMjksLTM2MzUxMzAwNCwt
ODc1MjY2ODM0LC0xMjMyOTA2MzczLC02NTI5NzE3MTUsMTY5Nj
A3MDI1NCwtMTUwODgzNDI0NywxNTE5MzA0OTQ5LDIwNTE3OTc1
OCwtOTI0MzkyOTE1LDE2OTI0MjM1NTUsNDQ2MTkwMzg5LDIwNT
g3ODY1MDldfQ==
-->