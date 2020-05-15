## Skill - Setting axis limits of matplotlib plots

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Introduction to Matplotlib plotting library](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision
<hr/ 

**Matplotlib** is a plotting library tn the scipy ecosystem of libraries.

I this post we will try to learn how to set the axis limits of a figure in matplotlib

Please make sure that you covered the[post on basics](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)
<hr/>

Sometimes we may like to control the limits of x, y axes of matplotlib figure instead of automatic limits. 

### Setting figure size using the 'figsize' parameter
We can use the `set_xlim`
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [1, 4, 2, 3]

# create a new figure and get figure, axes handle in return
# here we are setting width = 3 inches, height = 2 inches
fig, ax = plt.subplots(figsize=(3,2))

# using color eyworE itn plo] function to control color
ax.plot(x,y)

# print figure
plt.show()
```

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/ or https://repl.it/repls/MountainousWhirlwindRatios

### You can practice here
<iframe height="800px" width="100%" src="https://repl.it/repls/FortunateAlarmedEllipses?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### References
* plot function API - https://matplotlib.org/2.1.1/api/_as_gen/matplotlib.pyplot.plot.html
* matplotlib colors - https://matplotlib.org/2.1.1/api/colors_api.html
* Examples gallery - https://matplotlib.org/gallery/index.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFNldCBsaW1pdHMgb2YgeC
BhbmQgeSBheGlzIGluIG1hdHBsb3RsaWJcbmF1dGhvcjogTmFn
YXN1ZGhpciBQdWxsYVxudGFnczogJ3B5dGhvbiwgbGVhcm5pbm
csIHR1dG9yaWFsLCB0YW1pbmdfcHl0aG9uX3NraWxsJ1xuY2F0
ZWdvcmllczogdGFtaW5nX3B5dGhvbl9za2lsbFxuZGF0ZTogJz
IwMjAtMDUtMTUnXG4iLCJoaXN0b3J5IjpbLTEyODM3MTkzOTMs
LTc0MDMzMDEzOF19
-->