python notes -  http://thomas-cokelaer.info/tutorials/python/basics.html#the-basics

matplotlib overview tutorial - https://towardsdatascience.com/data-visualization-using-matplotlib-16f1aae5ce70


### TODOS
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



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg1MjAwNjAyNSwyMTIxNTc3MTQsLTc3ND
g2MDE0MywtNTIwNDcxOTM4LDczOTA3Mzc3OSwtOTYxNTgzNzgz
LC0xNjgzOTYxMzYsLTM0OTQ0ODM3MywxODgwMjAyODExLC0xMj
kyNDE0NzY5LDE2MzUwMDE4NjksLTE5MzkwNDc2ODcsMTkyMTAw
ODIyLC0zNTI5MjE2MCwxMTkwNDgwOTUwLC0xNDY5Nzk2ODM3XX
0=
-->