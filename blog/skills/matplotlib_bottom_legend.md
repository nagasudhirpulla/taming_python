## Skill - Matplotlib legend at the bottom of the plot
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

Please make sure that you covered the [post on basics](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)
<hr/>

In order to place the legend at the bottom using `ax.legend` function, we can use the following options

* `bbox_to_anchor` - location of the legend anchor w.r.t the plot bounding box. Anchor location is specified as (x,y)
* `loc` - Location of the legend anchor w.r.t legend box
* `ncol` - Max number of columns in the legend box
* `borderaxespad` - padding between axes and legend border in terms of font-size

```python
import matplotlib.pyplot as plt
import random

fig, ax = plt.subplots()
numLines = 5

for k in range(numLines):
    vals = [random.randint(0, 10) for x in range(4)]
    la,  = ax.plot([1, 2, 3, 4], vals)
    la.set_label("Another line {0}".format(k+1))

ax.legend(bbox_to_anchor=(0, -.1), loc='upper left',
          ncol=3, borderaxespad=0)

ax.set_title("Figure Title")

plt.show()
```

![matplotlib_bottom_legend_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_bottom_legend_demo.png)
### Video
You can the video on this post [here](https://youtu.be/CjLShBVPRbw)
<iframe width="560" height="315" src="https://www.youtube.com/embed/CjLShBVPRbw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/

### References
* Awesome blog post on legend placement - https://jdhao.github.io/2018/01/23/matplotlib-legend-outside-of-axes/
* Official legend function documentation - https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.legend.html#matplotlib.axes.Axes.legend

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MzM5NDMwODUsLTE3NjE5MDMzMzksLT
g4MTI1NzM5NSwtMTQ1NTA5NzU2Myw4NDc4NDA4NzksLTIxNDcx
NjkxMzUsNzgzOTcwMzQ2LDEwNTYxNzQ3NzIsMTgwODExNzUyOS
w0NTE2NjAwNDcsMTA2OTk4MTE4MF19
-->