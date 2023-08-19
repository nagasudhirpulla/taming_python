## Secondary axis and twin axis in python matplotlib plots

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Introduction to Matplotlib plotting library](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)
* [Styling Matplotlib plots](https://nagasudhir.blogspot.com/2020/05/styling-matplotlib-plots.html)

<hr/>

## Demo output

![matplotlib_secondary_axis_twinx_demo.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/matplotlib_secondary_axis_twinx_demo.png?raw=true)
## Sample code

```python
import matplotlib.pyplot as plt

# data for plotting
t = list(range(1, 11))
celciusVals = [20, 19, 19, 21, 23, 22, 21, 24, 20, 22]
salesVals = [98000, 80000, 76000, 85000,
             85000, 90000, 92000, 90000, 96000, 86000]

# create a figure and axes handle to plot celcius data
fig, ax1 = plt.subplots()

# plot celcius data
color = 'tab:red'
ax1.set_xlabel('days')
ax1.set_ylabel('centigrade temp', color=color)
ax1.plot(t, celciusVals, color=color)
ax1.tick_params(axis='y', labelcolor=color)

# conversion functions for fahrenheit axes
def celsius_to_fahrenheit(x):
    return x * 1.8 + 32  # x is of type numpy.ndarray, like array([18.75, 24.25])

def fahrenheit_to_celsius(x):
    return (x - 32) / 1.8

# derive a fahrenheit axes from celcius axes using secondary_yaxis
axFahren = ax1.secondary_yaxis(-0.25, functions=(celsius_to_fahrenheit, fahrenheit_to_celsius))

axFahren.set_ylabel('fahrenheit temp', color=color)
axFahren.tick_params(axis='y', labelcolor=color)

# create twin axes to celcius axes for plotting sales data
ax2 = ax1.twinx()  # shares the same x-axis with celsius axis

# plot sales data on the twin axis
color = 'tab:green'
ax2.set_ylabel('sales', color=color)  # we already handled the x-label with ax1
ax2.plot(t, salesVals, color=color)
ax2.tick_params(axis='y', labelcolor=color)

# export the figure as a png image
fig.tight_layout()
fig.savefig("output.png")
```

## Twin axis

-   Twin axis can be used to visually depict patterns or correlation between two plots even if they are of different scales
-   Twin axis can be used to display two plots with different scales so that both the plots are aligned
-   In the above example, the sales data and temperature data are shown on different axis. A new axis for showing temperature data is created using the `twinx` function.

## Secondary Y axis

-   A secondary Y axis can be derived from an existing axis using conversion functions
-   As shown in the example, a Fahrenheit axis can be derived from Celsius axis using the `secondary_yaxis` function
-   The conversion functions for primary to secondary axis values and secondary to primary axis values are to be mentioned

## References

-   Twinx function matplotlib - [](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.twinx.html#matplotlib-axes-axes-twinx)[https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.twinx.html#matplotlib-axes-axes-twinx](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.twinx.html#matplotlib-axes-axes-twinx)
-   Secondary y axis matplotlib - [](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.secondary_yaxis.html#matplotlib.axes.Axes.secondary_yaxis)[https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.secondary_yaxis.html#matplotlib.axes.Axes.secondary_yaxis](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.secondary_yaxis.html#matplotlib.axes.Axes.secondary_yaxis)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MjY1NTQxOSwtMjAzMjg3NDcyMSw0NT
AzNzQ4MDZdfQ==
-->