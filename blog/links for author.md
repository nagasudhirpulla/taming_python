python notes -  http://thomas-cokelaer.info/tutorials/python/basics.html#the-basics

matplotlib overview tutorial - https://towardsdatascience.com/data-visualization-using-matplotlib-16f1aae5ce70


### TODOS
* process dataframes from csv, excel and dbf in chunks
```python
import pandas as pd
import datetime as dt
maxVolume = 0
maxVolTs = 0
numRows = 0
volColName = "Volume_(Currency)"
for dfChunk in pd.read_csv("data.csv", chunksize=10000):
    numRows += len(dfChunk)
    tempMaxInd = dfChunk[volColName].idxmax()
    if (not pd.isna(tempMaxInd)):
        tempMax = dfChunk[volColName].loc[tempMaxInd]
        if tempMax > maxVolume:
            maxVolume = tempMax
            maxVolTs = dfChunk["Timestamp"].loc[tempMaxInd]
    print("{0} rows processed".format(numRows))
print("max volume was {0} at {1}".format(
    maxVolume, dt.datetime.fromtimestamp(maxVolTs)))
```
```python
for dfChunk in Dbf5(dbfPath).to_dataframe(chunksize=1000):  
	# process each dfChunk that contains 1000 rows in each dfChunk dataframe
```
* Histogram in python
* Manage application configuration or application secrets in Excel  
* global variables and using them inside functions- https://instructobit.com/tutorial/108/How-to-share-global-variables-between-files-in-Python
* python subprocess communication - https://eli.thegreenplace.net/2017/interacting-with-a-long-running-child-process-in-python/
* rounding of decimals while printing and rounding the number itself
* flask server basics
* naming conventions for classes (nouns), variables (nouns), functions (verbs), using camel case, avoid obvious names and use contextual names for better readability



<!--stackedit_data:
eyJoaXN0b3J5IjpbNDc5NzczMjM1LC02MTM1NTcxOTQsLTkyNz
UzMjQ5MSw3OTU3NjMzMzUsLTY1NjczNzk5NywtMTYzMjM5MjA4
NywtMjI5NjI5NTU3LDE5MjQyNjM5ODgsMTM5MTM5NDA2MCwxMj
U4Mjg2MjM3LC04OTAyMzkxMDAsLTExNDQ5MTE0MzcsLTM2NDU4
ODEzNiwtMTYwNzU1NjQ2OCwtMTE5Mzk4OTg3MCw5OTA1MTMxMT
EsLTg4MTEzODM4MSwtOTg5NDc3MjYxLC0yMDU2NDA1NTUwLC05
Nzg2NzM0MV19
-->