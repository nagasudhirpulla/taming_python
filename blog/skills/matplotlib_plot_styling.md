## Skill - Setting the Figure size of Matplotlib plots
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

In this post we will try to learn how to set the size of a figure in matplotlib

Please make sure that you covered the [post on basics](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)
<hr/>

Sometimes we may like to control the size of matplotlib figure instead of default figure size. This requirement may arise for saving figure as image etc

### Setting figure size using the 'figsize' parameter
Here we can see that  are providing `figsize` input to `subplots` function as 
`figsize=(width_in_inches, height_in_inches)`
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [1, 4, 2, 3]

# create a new figure and get figure, axes handle in return
# here we a
fig, ax = plt.subplots(figsize=(8,8))

# using color keyword in plot function to control color
ax.plot(x,y,color='magenta')

# print figure
plt.show()
```
![plot color demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_plot_color_demo.png)
<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/ or https://repl.it/repls/MountainousWhirlwindRatios

### Color example


### References
* plot function API - https://matplotlib.org/2.1.1/api/_as_gen/matplotlib.pyplot.plot.html
* matplotlib colors - https://matplotlib.org/2.1.1/api/colors_api.html
* Examples gallery - https://matplotlib.org/gallery/index.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFN0eWxpbmcgTWF0cGxvdG
xpYiBQbG90c1xuYXV0aG9yOiBOYWdhc3VkaGlyIFB1bGxhXG5k
YXRlOiAnMjAyMC0wNS0wOCdcbnRhZ3M6ICdweXRob24sIGxlYX
JuaW5nLCB0dXRvcmlhbCwgdGFtaW5nX3B5dGhvbl9za2lsbCdc
bmNhdGVnb3JpZXM6IHRhbWluZ19weXRob25fc2tpbGxcbiIsIm
hpc3RvcnkiOls3OTExMzczMjksNDg2OTE3MjYzLDU3NjY5Mjg5
NCwtMzI4ODU3MTA5LDMyMTQwMDYxMCwtMTM4MDA1MzcxMSwtMT
g2Mzg2MjEyNl19
-->