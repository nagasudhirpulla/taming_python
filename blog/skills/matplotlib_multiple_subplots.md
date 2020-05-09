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
use `nrows, ncols` parameters of the `plt.subplots` function to get a grid of subplots. 
This returns a figure and an array of axes handles in the same shape of the grid. That is, if the subplots grid is 3x2 then the shape of axes handles array will also be 3x2 
```python
import matplotlib.pyplot as plt

# suppose we want a figure with 3 rows 2 columns
# use nrows, ncols inputs to control the rows and columns of subplots
# constrained_layout parameter takes care of proper spacing
fig, axs = plt.subplots(nrows=3,ncols=2,constrained_layout=True)

# set entire figure title using the suptitle function
fig.suptitle('3 x 2 Subplot grid', fontsize=12)

# set titles for each subplot using the respective axes handles
axs[0][0].set_title('0,0 position')
axs[0][1].set_title('0,1 position')
axs[1][0].set_title('1,0 position')
axs[1][1].set_title('1,1 position')
axs[2][0].set_title('2,0 position')
axs[2][1].set_title('2,1 position')

# print the figure
plt.show()
```
![basic subplots grid output](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/basic_subplots_grid.PNG)
### Grid of subplots with uneven sizes
If the size of all the subplots in the grid is not same, then we need to use the `GridSpec` api to control how many rows and column each subplot will occupy in the subplot grid.
```python
import matplotlib.pyplot as plt

# just create the figure first and get the figure handle, we will add subplots later
fig = plt.figure(constrained_layout=True)

# create a grid spec for 3 rows and 3 columns
gspec = fig.add_gridspec(nrows=3, ncols=3)

# create a subplot in 0th row but occupying all the columns
# we are using add_subplot on the figure handle and getting the 
# subplot axis handle in return
ax0 = fig.add_subplot(gspec[0, :])
# set subplot title
ax0.set_title('gspec[0, :]')

# create a subplot in 1st row but occupying all the columns leaving the last column
ax1 = fig.add_subplot(gspec[1, :-1])
# set subplot title
ax1.set_title('gspec[1, :-1]')

# create a subplot in 1st row but occupying all the columns leaving the last column
ax1 = fig.add_subplot(gspec[1, :-1])
# set subplot title
ax1.set_title('gspec[1, :-1]')
```

Please take time to refer to this [official guide](https://matplotlib.org/3.1.0/tutorials/intermediate/gridspec.html) on creating matplotlib layouts with subplots for detailed and in depth explanation covering many use cases

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/ or https://repl.it/repls/MountainousWhirlwindRatios

### grid of subplots example
<iframe height="400px" width="100%" src="https://repl.it/repls/WryGummyMemwatch?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

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
1pbmdfcHl0aG9uX3NraWxsXG4iLCJoaXN0b3J5IjpbLTU2MDE3
MzI4MCwtNzY1ODA0NTAxLDE0NjE5MTc1NDYsLTczNTE0NjY2Mi
wxMzIzNDMzMjQ3LDMwNzkwNDU3Ml19
-->