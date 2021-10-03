## Skill - Save matplotlib plots into a pdf file
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

Please make sure that you covered the[post on basics](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)
<hr/>

In some cases we might want to create a single document that contains all the plots so that it can be easy shared with our friends.
Using ```PdfPages``` object of the ```matplotlib.backends.backend_pdf``` sub-module, mulitple figures can be inserted into a single pdf file

### Example
```python
from matplotlib.backends.backend_pdf import PdfPages
import matplotlib.pyplot as plt
import random

# create a pdf file object
pdfFile = PdfPages("output.pdf")

for pltItr in range(10):
    # create data for plot
    xVals = [x for x in range(1, 11)]
    yVals = [random.randint(50, 100) for x in xVals]

    # create a plot
    fig, ax = plt.subplots(figsize=(11,6))
    la, = ax.plot(xVals, yVals)
    ax.set_title("Plot number {0}".format(pltItr+1))
    ax.set_xlabel("X Values")
    ax.set_ylabel("Y Values")
    fig.tight_layout(pad=4)

    # add figure to pdf file
    pdfFile.savefig(fig)

# close the pdf file
pdfFile.close()
```

### Video
You can the video on this post [here](https://youtu.be/NVU669QpL-g)

<iframe width="560" height="315" src="https://www.youtube.com/embed/NVU669QpL-g" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

## References
* Matplotlib tight layout guide - https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.tight_layout.html#matplotlib.pyplot.tight_layout

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgzMTc0MTAwOSwtNTkxMzUxNzU1LC0xMz
g1NDIwMzIzLC0xMzAyNzg2Mjg3LC0zMDU0MjkyNzgsLTEzMzYy
Mjc1ODEsNDY3ODQ0ODIwXX0=
-->