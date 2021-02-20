python notes -  http://thomas-cokelaer.info/tutorials/python/basics.html#the-basics

matplotlib overview tutorial - https://towardsdatascience.com/data-visualization-using-matplotlib-16f1aae5ce70


### TODOS
* change dataframe dimensions using pivot and melt
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

def deriveDurationVals(vals, resol):
    min_value = vals.min()
    max_value = vals.max()
    binVals = []
    perc_time_exceeded = []
    numVals = len(vals)   
    
    for val in np.arange(min_value, max_value, resol):
        binVals.append(val)
        perc_exceeded = len(vals[vals>val])*100/numVals
        perc_time_exceeded.append(perc_exceeded)

    return {'bins': binVals, 'perc_exceeded': perc_time_exceeded}
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
eyJoaXN0b3J5IjpbOTI2Nzk1MzA0LC0zOTg1NDI2MDAsMTE3Mj
IzNjI4MywxODUyMDA2MDI1LDIxMjE1NzcxNCwtNzc0ODYwMTQz
LC01MjA0NzE5MzgsNzM5MDczNzc5LC05NjE1ODM3ODMsLTE2OD
M5NjEzNiwtMzQ5NDQ4MzczLDE4ODAyMDI4MTEsLTEyOTI0MTQ3
NjksMTYzNTAwMTg2OSwtMTkzOTA0NzY4NywxOTIxMDA4MjIsLT
M1MjkyMTYwLDExOTA0ODA5NTAsLTE0Njk3OTY4MzddfQ==
-->