## Skill - Export a Matplotlib figure as an image or a pdf file
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

In this post we will try to understand how to export a matplotlib figure as an image or pdf file

Please make sure that you covered the [post on basics](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)

<hr/>

### Using "savefig" method to save the figure as a file
```python
import matplotlib.pyplot as plt

# create a plotting area and get the figure, axes handle in return
fig, ax = plt.subplots()

# plot some data
ax.plot([0,4,8,12], [6,8,4,2])
ax.plot([0,3,9,12,15,18], [2,1,9,6,4,3])

# save figure as a png file
fig.savefig("output.png")
fig.savefig(r"C:\figure.jpg")
fig.savefig(r"C:\testFile.pdf")
```
![basic multiple plots output](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/basic_multiple_plots.png)
As shown in the above code, just by using the ```savefig``` method on a matplotlib figure, we can export the figure as a pdf or image file. 

Note that we can also provide an absolute file path like ```C:\testFile.pdf``` so that the file can be stored in any desired location of the computer

### Video
You can the video on this post [here](https://youtu.be/qpVhubsBcdk)

<iframe width="560" height="315" src="https://www.youtube.com/embed/qpVhubsBcdk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<hr/>

### References
*  savefig documentation - https://matplotlib.org/stable/api/figure_api.html#matplotlib.figure.Figure.savefig

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc1NDAyMDY3MywtMTU4NTY4NzA5MywtOD
k4Mjc3MDQyLC0xNjA4MDg1MDc0XX0=
-->