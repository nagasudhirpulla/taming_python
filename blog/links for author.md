python notes -  http://thomas-cokelaer.info/tutorials/python/basics.html#the-basics

matplotlib overview tutorial - https://towardsdatascience.com/data-visualization-using-matplotlib-16f1aae5ce70


### TODOS
* matplotlib legend at the bottom of plot
```python
# %%
import matplotlib.pyplot as plt
import random

# create figure and axes
fig, ax = plt.subplots(figsize=(11, 6))

# set plot title ans axis labels
ax.set_title("Bottom Legend Example")
ax.set_xlabel("X axis values")
ax.set_ylabel("Random numbers")

# x axis values
xVals = [x for x in range(20)]

for pltItr in range(5):
    # create random y axis values
    yVals = [random.randint(50, 100) for x in xVals]
    # create a line plot with x and y values
    la, = ax.plot(xVals, yVals)
    # set plot label for legend
    la.set_label("Trace {0}".format(pltItr+1))

# enable legend with bottom positioning
ax.legend(loc='upper center', bbox_to_anchor=(0.5, -0.1),
          shadow=True, ncol=5)

# adjust layout elements along with adding outer padding as 1 inch
fig.tight_layout(pad=1)

# save the figure as a png file
fig.savefig("output.png")
# %%
```
* docxtpl tutorial for templates, plots, images etc
* Histogram in python
* Manage application configuration or application secrets in Excel  
* global variables and using them inside functions- https://instructobit.com/tutorial/108/How-to-share-global-variables-between-files-in-Python
* python subprocess communication - https://eli.thegreenplace.net/2017/interacting-with-a-long-running-child-process-in-python/
* rounding of decimals while printing and rounding the number itself
* flask server basics
* naming conventions for classes (nouns), variables (nouns), functions (verbs), using camel case, avoid obvious names and use contextual names for better readability



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NTExODQzODQsMTM5MTM5NDA2MCwxMj
U4Mjg2MjM3LC04OTAyMzkxMDAsLTExNDQ5MTE0MzcsLTM2NDU4
ODEzNiwtMTYwNzU1NjQ2OCwtMTE5Mzk4OTg3MCw5OTA1MTMxMT
EsLTg4MTEzODM4MSwtOTg5NDc3MjYxLC0yMDU2NDA1NTUwLC05
Nzg2NzM0MSwtMzIzOTg4MTQ5LC0xOTIzNzYzOTQ3LDM5NDUzNz
g2OSwtMTM5MTQ5NTYwNSwtMjIxODg5OTc1LDY2MTY3NDAxNCw5
MjY3OTUzMDRdfQ==
-->