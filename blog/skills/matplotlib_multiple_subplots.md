## Skill - Multiple Subplots in a figure using Matplotlib
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Introduction to Matplotlib plotting library](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)
* [Styling Matplotlib plots](https://nagasudhir.blogspot.com/2020/05/styling-matplotlib-plots.html)
* [Multiple Plots in a same subplot using Matplotlib](https://nagasudhir.blogspot.com/2020/05/multiple-plots-in-same-subplot-using.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/>

**Matplotlib** is a plotting library in the scipy ecosystem of libraries.

In this post we will learn how to plot multiple subplots on a single Matplotlib figure

<hr/>

### Creating a grid of subplots
```python
import matplotlib.pyplot as plt

# suppose we want a figure with 3 rows 2 columns
# use nrows, ncols inputs to control the rows and columns of subplots
# constrained_layout parameter takes care of proper spacing
fig, axs = plt.subplots(nrows=3,ncols=2,constrained_layout=True)

# set figure title
fig.suptitle()

# set titles
axs[0][0].set_title('0,0 position')
axs[0][1].set_title('0,1 position')
axs[1][0].set_title('1,0 position')
axs[1][1].set_title('1,1 position')
axs[2][0].set_title('2,0 position')
axs[2][1].set_title('2,1 position')

```

Please take time to refer to this [official guide](https://matplotlib.org/3.1.0/tutorials/intermediate/gridspec.html) on creating matplotlib layouts with subplots for detailed and in depth explanation covering many use cases

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/ or https://repl.it/repls/MountainousWhirlwindRatios

### Multiple plots example
<iframe src="https://trinket.io/embed/python3/3bc5748621" width="100%" height="356" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

### Styled multiple plots example
<iframe src="https://trinket.io/embed/python3/93046401c2" width="100%" height="356" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

### References
*  subplot layouts official guide - https://matplotlib.org/3.1.0/tutorials/intermediate/gridspec.html
* another post - https://towardsdatascience.com/data-visualization-using-matplotlib-16f1aae5ce70
* Examples gallery - https://matplotlib.org/gallery/index.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)



<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IE11bHRpcGxlIHN1YnBsb3
RzIGluIGEgZmlndXJlIHVzaW5nIE1hdHBsb3RsaWJcbmF1dGhv
cjogTmFnYXN1ZGhpciBQdWxsYVxuZGF0ZTogJzIwMjAtMDUtMD
knXG50YWdzOiAncHl0aG9uLCBsZWFybmluZywgdHV0b3JpYWws
IHRhbWluZ19weXRob25fc2tpbGwnXG5jYXRlZ29yaWVzOiB0YW
1pbmdfcHl0aG9uX3NraWxsXG4iLCJoaXN0b3J5IjpbMjA2NTg3
MjExOCwxNDYxOTE3NTQ2LC03MzUxNDY2NjIsMTMyMzQzMzI0Ny
wzMDc5MDQ1NzJdfQ==
-->