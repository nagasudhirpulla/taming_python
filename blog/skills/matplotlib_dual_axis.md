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
import datetime as dt

t = list(range(1, 11))
tempVals = [20, 19, 19, 21, 23, 22, 21, 24, 20, 22]
salesVals = [98000, 80000, 76000, 85000, 85000, 90000, 92000, 90000, 96000, 86000]

fig, ax1 = plt.subplots()

color = 'tab:red'
ax1.set_xlabel('days')
ax1.set_ylabel('centigrade temp', color=color)
ax1.plot(t, tempVals, color=color)
ax1.tick_params(axis='y', labelcolor=color)

def celsius_to_fahrenheit(x):
    return x * 1.8 + 32

def fahrenheit_to_celsius(x):
    return (x - 32) / 1.8

axFahren = ax1.secondary_yaxis(-0.25, functions=(celsius_to_fahrenheit, fahrenheit_to_celsius))

axFahren.set_ylabel('fahrenheit temp', color=color)
axFahren.tick_params(axis='y', labelcolor=color)

ax2 = ax1.twinx()  # instantiate a second axes that shares the same x-axis

color = 'tab:green'
ax2.set_ylabel('sales', color=color)  # we already handled the x-label with ax1
ax2.plot(t, salesVals, color=color)
ax2.tick_params(axis='y', labelcolor=color)

fig.tight_layout()
fig.savefig("output.png")
```


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
eyJoaXN0b3J5IjpbLTcxMjgyMzMzMCw0NTAzNzQ4MDZdfQ==
-->