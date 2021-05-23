## Skill - Duration Plot in Matplotlib
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Functions in python](https://nagasudhir.blogspot.com/2020/05/fucntions-in-python.html)
* [Introduction to Matplotlib plotting library](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)
* [Styling Matplotlib plots](https://nagasudhir.blogspot.com/2020/05/styling-matplotlib-plots.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

**Matplotlib** is a plotting library tn the scipy ecosystem of libraries.

Please make sure that you covered the[post on basics](https://nagasudhir.blogspot.com/2020/05/intro-to-matplotlib.html)
<hr/>
Duration Plot helps us visualize the sample frequency distribution in a single plot.

### Duration Plot values derivation function
```python
import numpy as np
import pandas as pd

def deriveDurationVals(vals, valBinResol):
    samplVals = []
    percExceeded = []
    vals = pd.Series(vals)
    numVals = len(vals)
    min_value = vals.min()
    max_value = vals.max()

    for val in np.arange(min_value, max_value, valBinResol):
        samplVals.append(val)
        binExceededPerc = len(vals[vals > val])*100/numVals
        percExceeded.append(binExceededPerc)

    return {'sampl_vals': samplVals, 'perc_exceeded': percExceeded}
```

### Example of duration plot
In the sample  folder containing the example script, create a file named ```duration_plot.py``` and write the function shown above and use the function in the example as shown below
```python
import matplotlib.pyplot as plt
from duration_plot import deriveDurationVals

sampls = [50.061,50.055,50.043,50.050,...]
durPltData = deriveDurationVals(sampls, 0.01)
fig, ax = plt.subplots()
ax.plot(durPltData["perc_exceeded"], durPltData["sampl_vals"])
plt.show()
```
![matplotlib_duration_plot_demo](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/img/matplotlib_duration_plot.png)

### Video
You can the video on this post [here](https://youtu.be/QYBAP0YxSZU)

<iframe width="560" height="315" src="https://www.youtube.com/embed/QYBAP0YxSZU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<hr/>

### Online Interpreter
Although we recommend to practice the above examples in Visual Studio Code, you can run these examples online at https://pynative.com/online-python-code-editor-to-execute-python-code/ or https://repl.it/repls/MountainousWhirlwindRatios

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5ODE5NTI0MzAsMTA1MDAxNDU0NCwtMT
U2OTYxODY1MSwtMTc2NjM1MTE5M119
-->