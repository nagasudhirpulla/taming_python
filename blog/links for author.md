python notes -  http://thomas-cokelaer.info/tutorials/python/basics.html#the-basics

matplotlib overview tutorial - https://towardsdatascience.com/data-visualization-using-matplotlib-16f1aae5ce70


### TODOS
* process dataframes and dbf in chunks
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
eyJoaXN0b3J5IjpbLTE4MTY5MTE3NzAsLTYxMzU1NzE5NCwtOT
I3NTMyNDkxLDc5NTc2MzMzNSwtNjU2NzM3OTk3LC0xNjMyMzky
MDg3LC0yMjk2Mjk1NTcsMTkyNDI2Mzk4OCwxMzkxMzk0MDYwLD
EyNTgyODYyMzcsLTg5MDIzOTEwMCwtMTE0NDkxMTQzNywtMzY0
NTg4MTM2LC0xNjA3NTU2NDY4LC0xMTkzOTg5ODcwLDk5MDUxMz
ExMSwtODgxMTM4MzgxLC05ODk0NzcyNjEsLTIwNTY0MDU1NTAs
LTk3ODY3MzQxXX0=
-->