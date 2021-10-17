## Skill - Read and process pandas dataframes from large files using chunks
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

#### Skills Required
* [Setup python development environment](https://nagasudhir.blogspot.com/2020/04/setup-python-development-environment_14.html)
* [Basic Printing in Python](https://nagasudhir.blogspot.com/2020/04/basic-printing-in-python.html)
* [Commenting in Python](https://nagasudhir.blogspot.com/2020/04/comments-in-python.html)
* [Managing Variables in python](https://nagasudhir.blogspot.com/2020/04/managing-variables-in-python.html)
* [Pandas DataFrame Basics](https://nagasudhir.blogspot.com/2020/05/pandas-dataframe-basics.html)

Please make sure to have all the skills mentioned above to understand and execute the code mentioned below. Go through the above skills if necessary for reference or revision

<hr/>

* If we try to import large a csv or dbf file into a single dataframe, we may run into memory issues resulting in crashing of the python script.
* In this post we will process large dataframe from large data file using ```chunksize``` option while importing the data.
*  Using ```chunksize``` option returns an iterator that reads a huge data file as chunks of dataframes with each dataframe chunk having number of rows equal to ```chunksize``` (For example chunksize can be 10,000 rows).
* If we desire to import dataframe from dbf file, we require simpledbf module. Install it using the command `pip install simpledbf`

### Example Code
* The below example python script processes a huge csv file containing historical bitcoin data in chunks of 10,000 rows 
* Each dataframe chunk is processed to update the maximum bitcoin volume and the timestamp at maximum volume
* The csv file used in this example can be downloaded from [here](https://www.kaggle.com/mczielinski/bitcoin-historical-data)

```python
import  pandas  as  pd
import  datetime  as  dt
df = pd.read_csv("data.csv", nrows=10)
print(df.columns.tolist())

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

Thus by using a divide and rule approach, we can process a huge data file using the ```chunksize``` option while importing the file

### .dbf file example code
The file used in this example can be downloaded from [here](https://github.com/nagasudhirpulla/taming_python/raw/master/blog/skills/assets/data/marks.dbf)
```python
import  pandas  as  pd
import  datetime  as  dt
from simpledbf import Dbf5

# path of dbf file
dbfPath = 'test.dbf'
numRows = 0
for dfChunk in Dbf5(dbfPath).to_dataframe(chunksize=10):  
	# process each dataframe chunk
	numRows += len(dfChunk)
	print("processed {0} rows".format(numRows))
```

<hr/>

### References
* https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyNDkyNDQ1MjJdfQ==
-->