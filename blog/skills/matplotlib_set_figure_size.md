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

**Matplotlib** is a plotting library tn the scipy ecosystem of libraries.

I this post we will try to learn  how to set the size of a figure in matplotlib

Please make sure that you covered the[post on basics](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)
<hr/>

Sometimes we may like to control the size of matplotlib figure instead of default figure size. This requirement may arise for saving figure as image etc

### Setting figure size using the 'figsize' parameter
Here we are providing `figsize` input to `subplots` function as 
`figsize=(width_in_inches, height_in_inches)`
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [1, 4, 2, 3]

# create a new figure and get figure, axes handle in return
# here we are setting width = 3 inches, height = 2 inches
fig, ax = plt.subplots(figsize=(3,2))

# using color keyword itn plot function to control color
ax.plot(x,y)

# print figure
plt.show()
```

### Video
You can the video on this post [here](https://youtu.be/DeLQNy-jiwE)

<iframe width="560" height="315" src="https://www.youtube.com/embed/DeLQNy-jiwE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/

### References
* plot function API - https://matplotlib.org/2.1.1/api/_as_gen/matplotlib.pyplot.plot.html
* matplotlib colors - https://matplotlib.org/2.1.1/api/colors_api.html
* Examples gallery - https://matplotlib.org/gallery/index.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFNldHRpbmcgRmlndXJlIH
NpemUgb2YgbWF0cGxvdGxpYiBwbG90c1xuYXV0aG9yOiBOYWdh
c3VkaGlyIFB1bGxhXG5kYXRlOiAnMjAyMC0wNS0xMydcbnRhZ3
M6ICdweXRob24sIGxlYXJuaW5nLCB0dXRvcmlhbCwgdGFtaW5n
X3B5dGhvbl9za2lsbCdcbmNhdGVnb3JpZXM6IHRhbWluZ19weX
Rob25fc2tpbGxcbiIsImhpc3RvcnkiOlsxNDUwNTc5Nzc0LDQ1
MjEwMjkxMiwtMTQzNzkwNTQ5OSwtMTk5OTU5NjkyNSwtMjEzOT
YyMTI5NCwtMjEwMDkyMTcwMCwtMTU2MDQwMjAyMywtMTM3NjI5
MTcyM119
-->