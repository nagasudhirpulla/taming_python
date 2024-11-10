# Import / Export Pandas dataframes to SQLite database

-   SQLite is a file based relational database. So an SQLite database would be a single file like csv or excel file
-   In addition to CSV or excel, pandas dataframes can be exported to SQLite database for persisting or sharing the dataframes. This approach is useful when working with large number of rows

## Sample SQLite database

The sample SQLite database `iris.db` can be downloaded at [https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/data/iris.db](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/data/iris.db)

## Read data as dataframe from SQLite with an SQL query

-   A method `pd.read_sql_query(sqlString, sqliteConnectionObject)` can be used to create a dataframe from SQL query as shown below

```python
import sqlite3
import pandas as pd

# Create connection with SQLite database
con = sqlite3.connect("data/iris.db")

# create a dataframe from sqlQuery
sqlQuery = """
SELECT sp.species, 
max(ob.petal_length) as maxPetalLength, 
count(ob.sepal_length) as numSamples 
FROM Observation ob
left join Species sp on sp.species_id=ob.species_id
group by ob.species_id
"""
df = pd.read_sql_query(sqlQuery, con)

print(df)
```

## Write dataframe into an SQLite database table

-   Dataframe rows can be inserted into an SQLite database table by calling the `to_sql` method on the dataframe. For example: `df.to_sql("tableName", sqliteConnectionObject, if_exists="append", index=False)`
    -   The argument `if_exists="fail"` (default) will raise error if SQLite table is already present
    -   The argument `if_exists="append"` will add new rows to SQLite table (if present)
    -   The argument `if_exists="replace"` will replace all rows of SQLite table (if present) with dataframe rows
    -   The argument `index=False` will not write the dataframe index into the SQLite table
-   The example below appends a dataframe into an SQLite table using `to_sql` method on dataframe

```python
import sqlite3
import pandas as pd
import datetime as dt

# Create connection with SQLite database
con = sqlite3.connect("data/iris.db")

# create dataframe with the rows to be inserted in SQLite table
# column names of dataframe should match with table
df = pd.DataFrame([
    {"time": dt.datetime.now()-dt.timedelta(minutes=1),
     "temperature": 23, "windSpeedKmph": 6},
    {"time": dt.datetime.now()-dt.timedelta(minutes=6),
     "temperature": 22, "windSpeedKmph": 5.3},
    {"time": dt.datetime.now()-dt.timedelta(minutes=11),
     "temperature": 24, "windSpeedKmph": 5.8},
])
print(df)

# add dataframe data to an sqlite table
# if_exists can be "append", "replace", "fail"
df.to_sql("weatherData", con, if_exists="append",
          index=False)
```

-   Another example below creates a dataframe from and SQL that analyses the database information. The dataframe is again persisted into the database for future reference.

```python
import sqlite3
import pandas as pd

# Create connection with SQLite database
con = sqlite3.connect("data/iris.db")

# create a dataframe from sqlQuery
sqlQuery = """
SELECT sp.species, 
max(ob.petal_length) as maxPetalLength, 
count(ob.sepal_length) as numSamples 
FROM Observation ob
left join Species sp on sp.species_id=ob.species_id
group by ob.species_id
"""
df = pd.read_sql_query(sqlQuery, con)

print(df)

# write dataframe results to an sqlite table
# if_exists can be "append", "replace", "fail"
df.to_sql("speciesSummary", con, if_exists="replace")
```

## Read dataframe as chunks for large data queries

-   While reading large number of rows, an additional parameter `chunksize` can be specified to fetch data from SQLite query in dataframe chunks of specified size. For example, `pd.read_sql_query("select * from Observation", con, chunksize=60)`
-   The data will not be loaded into memory at once, instead data will be fetched from database at each iteration as shown below

```python
import sqlite3
import pandas as pd

# Create connection with SQLite database
con = sqlite3.connect("data/iris.db")

# read SQL query results as dataframe chunks
for chunkIter, dfChunk in enumerate(pd.read_sql_query("select * from Observation", con, chunksize=60)):
    print(f"printing chunk {chunkIter} of size {len(dfChunk)}")
    print(dfChunk)
```

## Parameter substitution while querying data

-   The example below substitutes a parameter `:sId` using the params option of the `read_sql_query` method

```python
import sqlite3
import pandas as pd

# Create connection with SQLite database
con = sqlite3.connect("data/iris.db")

# create a dataframe from sqlQuery
sqlQuery = """
SELECT max(ob.sepal_length) as maxSepalWidth 
FROM Observation ob
where species_id=:sId
"""
df = pd.read_sql_query(sqlQuery, con, params={"sId": 1})
print(df)

print(f"max sepal width is {df.iloc[0][0]}")
```

## Other useful query options

Some useful options that can be used in the `read_sql_query` method are as follows

-   `index_col` option can specify the column/list of columns to be considered as dataframe index
-   `parse_dates` option can specify the columns to be parsed as datetime object. For example:

```python
df = pd.read_sql_query("select * from weatherData", con,
                       parse_dates={"time":"%Y-%m-%d %H:%M:%S.%f"})
# or else
df = pd.read_sql_query("select * from weatherData", con,
                       parse_dates=["time"])
```

## References

-   read_sql_query docs - [https://pandas.pydata.org/docs/reference/api/pandas.read_sql_query.html](https://pandas.pydata.org/docs/reference/api/pandas.read_sql_query.html)
-   to_sql docs - [https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_sql.html](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_sql.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU4Njg1Mzg3MV19
-->