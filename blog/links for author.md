python notes -  http://thomas-cokelaer.info/tutorials/python/basics.html#the-basics

matplotlib overview tutorial - https://towardsdatascience.com/data-visualization-using-matplotlib-16f1aae5ce70


### TODOS
* change dataframe dimensions using pivot and melt
* matplotlib export figure as pdf or image
* matplotlib bottom legend and multiple lines in figure title - https://github.com/dheerajgupta0001/wrldc_mis_monthly_report_generator/blob/ed3ddd19bd2e71a956e0880b222cf5eb4f6a8cf3/src/app/section_1_4/section_1_4_2.py#L76
* python data structures lists and dictionaries
* in keyword in python
* bubble map geographic plots using folium 
* Duration curve in python  
```python
'''
Function inputs – list of values
Resolution of duration plot
Output – bin values, percentage exceeded
'''
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from data import sampls

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

durPltData = deriveDurationVals(sampls, 0.01)

fig, ax = plt.subplots()
ax.plot(durPltData["perc_exceeded"], durPltData["sampl_vals"])
plt.show()
```
* Histogram in python
* Manage application configuration or application secrets in Excel  
* global variables and using them inside functions- https://instructobit.com/tutorial/108/How-to-share-global-variables-between-files-in-Python
* python subprocess communication - https://eli.thegreenplace.net/2017/interacting-with-a-long-running-child-process-in-python/
* rounding of decimals while printing and rounding the number itself
* flask server basics
* virtual environments concept and practical use
* naming conventions for classes (nouns), variables (nouns), functions (verbs), using camel case, avoid obvious names and use contextual names for better readability



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIyMTg4OTk3NSw2NjE2NzQwMTQsOTI2Nz
k1MzA0LC0zOTg1NDI2MDAsMTE3MjIzNjI4MywxODUyMDA2MDI1
LDIxMjE1NzcxNCwtNzc0ODYwMTQzLC01MjA0NzE5MzgsNzM5MD
czNzc5LC05NjE1ODM3ODMsLTE2ODM5NjEzNiwtMzQ5NDQ4Mzcz
LDE4ODAyMDI4MTEsLTEyOTI0MTQ3NjksMTYzNTAwMTg2OSwtMT
kzOTA0NzY4NywxOTIxMDA4MjIsLTM1MjkyMTYwLDExOTA0ODA5
NTBdfQ==
-->