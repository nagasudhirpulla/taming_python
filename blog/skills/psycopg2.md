## Skill - Using psycopg2 python module for PostgreSQL interfacing
[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)

<hr/>
In this post we will use psycopg2 python module for interfacing with PostgreSQL database.

## Installing psycopg2 python module
Run the following command in your python environment
```
python -m pip install psycopg2
``` 

## Connecting to a database
The required parameters for connecting to a postgreSQL database are
* database server host (example: localhost / 192.168.19.5)
* database server listening port (example: 5432)
* database name (example: test_db)
* database username (example: postgres)
* database password (example: p#ssw0rd)

```python
import psycopg2

hostStr = 'localhost'
dbPort = 5433
dbStr = 'test1'
uNameStr = 'postgres'
dbPassStr = 'pass'

try:
    conn = psycopg2.connect(host=hostStr, port=dbPort, dbname=dbStr, user=uNameStr, password=dbPassStr)

    # get a cursor object from the connection
    cur = conn.cursor()

    # use the cursor object to run SQL commands to perform operations like fetch rows, insert rows, update rows, delete rows etc.
except (Exception, psycopg2.Error) as error:
    print("Error while interacting with PostgreSQL", error)
    records = 0
finally:
    if(conn):
        # close the cursor object to avoid memory leaks
        cur.close()
        # close the connection object also
        conn.close()
```

* The above python program uses a connection object and a cursor object.
* **Connection object** establishes connection with the database.
* **Cursor object** uses the connection object to execute SQL commands in the database to update data or fetch data from the database.
* Cursors can also perform transactions for atomic execution of multiple commands. That means either all SQL commands will be executed, or else all the SQL commands will be cancelled.

## Fetching data from database

```python
import psycopg2
import datetime as dt
import pandas as pd

hostStr = 'localhost'
dbPort = 5433
dbStr = 'test1'
uNameStr = 'postgres'
dbPassStr = 'pass'

try:
    conn = psycopg2.connect(host=hostStr, port=dbPort, dbname=dbStr,
                            user=uNameStr, password=dbPassStr)

    # get a cursor object from the connection
    cur = conn.cursor()

    # sql command to be executed for fetching the data
    sqlStr = "select name, dob, studentid from public.students \
        where dob >= %s and studentid > %s \
        order by name, studentid"

    # execute the data fetch command along with the SQL placeholder values
    cur.execute(sqlStr, (dt.datetime(2018, 1, 1, 0, 0, 0), 3000))

    # fetch all the records from cursor
    records = cur.fetchall()
    # get the column names of the fetched records
    colNames = [row[0] for row in cur.description]

    # iterate through all the fetched records
    for rowIter in range(len(records)):
        print("reading data from {0} row".format(rowIter))
        rowTuple = records[rowIter]
        print("name =", rowTuple[0])
        print("dob =", rowTuple[1])
        print("studentId =", rowTuple[2])

    # create a dataframe from the fetched records (optional)
    recordsDf = pd.DataFrame.from_records(records, columns=colNames)
except (Exception, psycopg2.Error) as error:
    print("Error while interacting with PostgreSQL", error)
    records = []
finally:
    if(conn):
        # close the cursor object to avoid memory leaks
        cur.close()
        # close the connection object also
        conn.close()

print("data fetch example code execution complete...")
```

* In the above code we have create an SQL fetch command to be executed as a string.

```python
sqlStr = "select name, dob, studentid from public.students \
where dob >= %s and studentid > %s \
order by name, studentid"
```

* We have also given SQL input placeholders as ```%s``` to inject python variables into SQL statement while execution. This is a strongly recommended way of inserting variables in SQL commands since this avoids SQL injection attacks in our python programs.
* ```cur.fetchall()``` will return the results of SQL fetch query as a list of tuples from our cursor variable.
* ```[row[0] for row in cur.description]``` will return the column names in order for the fetched list of data tuples. 

## Insert rows example
```python
```
### References
* psycopg2 documentation - https://www.psycopg.org/docs/usage.html
* PostgreSQL Official docs - https://www.postgresql.org/docs/14/index.html
* pgAdmin download - https://www.pgadmin.org/download/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg2MDcxNjI2NSw2OTgwOTY0NzMsNzUyMz
kwNzQ1LDQwODE4MDc3LDE0NDg0NjkxNCwtMTUzNjc2NzgzMiwt
MjEzMTIxMTM3MCwyMDQ0ODUzMTcsMTk3OTg4MTM2MCwtMTM2ND
I1MTQyOSwxMDI3MTIwMjI0LC0xMTUzNjcxNTgyXX0=
-->