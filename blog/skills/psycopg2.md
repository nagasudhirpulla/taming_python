## Skill - psycopg2 python module for PostgreSQL database interfacing
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
# initialize the connection object
conn=None
try:
    conn = psycopg2.connect(host=hostStr, port=dbPort, dbname=dbStr, user=uNameStr, password=dbPassStr)

    # get a cursor object from the connection
    cur = conn.cursor()

    # use the cursor object to run SQL commands to perform operations like fetch rows, insert rows, update rows, delete rows etc.
except (Exception, psycopg2.Error) as error:
    print("Error while interacting with PostgreSQL...\n", error)
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

## SQL to create the table used in this blog post
* The example codes given below require a table called ```students``` in the postgreSQL database. 
* Please run the below SQL in your database to create the required table
```sql
-- public.students definition

-- Drop table
-- DROP TABLE public.students;

CREATE TABLE public.students (
	id serial4 NOT NULL,
	name varchar(250) NOT NULL,
	dob timestamp NOT NULL,
	studentid int4 NOT NULL,
	CONSTRAINT name_unique_students UNIQUE (name, dob),
	CONSTRAINT students_pkey PRIMARY KEY (id),
	CONSTRAINT "students_un_studentId" UNIQUE (studentid)
);
```

## Fetching rows from database example

```python
import psycopg2
import datetime as dt
import pandas as pd

hostStr = 'localhost'
dbPort = 5433
dbStr = 'test1'
uNameStr = 'postgres'
dbPassStr = 'pass'
# initialize the connection object
conn=None
try:
    conn = psycopg2.connect(host=hostStr, port=dbPort, dbname=dbStr, user=uNameStr, password=dbPassStr)

    # get a cursor object from the connection
    cur = conn.cursor()

    # sql command to be executed for fetching the data
    sqlStr = "select name, dob, studentid from public.students \
        where dob >= %s and studentid > %s \
        order by name, studentid"

    # execute the data fetch SQL command along with the SQL placeholder values
    cur.execute(sqlStr, (dt.datetime(2018, 1, 1, 0, 0, 0), 3000))

    rowCount = cur.rowcount
    print("number of fetched rows =", rowCount)

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
    print("Error while interacting with PostgreSQL...\n", error)
    records = []
finally:
    if(conn):
        # close the cursor object to avoid memory leaks
        cur.close()
        # close the connection object also
        conn.close()

print("data fetch example code execution complete...")
```

* In the above code we have created an SQL fetch command to be executed as a string.

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
import psycopg2
import datetime as dt
import pandas as pd

hostStr = 'localhost'
dbPort = 5433
dbStr = 'test1'
uNameStr = 'postgres'
dbPassStr = 'pass'
# initialize the connection object
conn=None
try:
    conn = psycopg2.connect(host=hostStr, port=dbPort, dbname=dbStr, user=uNameStr, password=dbPassStr)

    # get a cursor object from the connection
    cur = conn.cursor()

    # prepare data insertion rows
    dataInsertionTuples = [
        ('xyz', dt.datetime(2021, 1, 1), 7654),
        ('abc', dt.datetime(2020, 10, 12), 9724)
    ]

    # create sql command for rows insertion
    dataText = ','.join(cur.mogrify('(%s,%s,%s)', row).decode(
        "utf-8") for row in dataInsertionTuples)

    sqlTxt = 'INSERT INTO public.students(\
                name, dob, studentid)\
                VALUES {0} on conflict (studentid) \
                do update set name = excluded.name, dob=excluded.dob'.format(dataText)

    # execute the sql to perform insertion
    cur.execute(sqlTxt)

    rowCount = cur.rowcount
    print("number of inserted rows =", rowCount)

    # commit the changes
    conn.commit()
except (Exception, psycopg2.Error) as error:
    print("Error while interacting with PostgreSQL...\n", error)
finally:
    if(conn):
        # close the cursor object to avoid memory leaks
        cur.close()
        # close the connection object also
        conn.close()

print("data insertion example code execution complete...")
```
* In the above program, we have used ```cur.mogrify``` function to convert python variables like strings, numnbers, datetime objects into SQL command strings. This is very important because SQL injection issue will be addresses by using the ```cur.mogrify``` function. Do not  convert variables to strings by yourself. Let psycopg2 handle the string conversion.
* We have used ```ON CONFLICT DO UPDATE``` clause in the insert SQL statement. This helps in easily handling the situations without errors where duplicate rows are trying to get inserted.
* The ```conn.commit()``` function is committing all the uncommitted database changes made by the cursor object by executing SQL commands. Without calling this function, the database changes made by the cursor object will not be permanent. Hence do not forget to call ```conn.commit``` after executing a database modification command like INSERT, DELETE, UPDATE.

## Delete rows example

```python
import psycopg2
import datetime as dt
import pandas as pd

hostStr = 'localhost'
dbPort = 5433
dbStr = 'test1'
uNameStr = 'postgres'
dbPassStr = 'pass'
# initialize the connection object
conn=None
try:
    conn = psycopg2.connect(host=hostStr, port=dbPort, dbname=dbStr,
                            user=uNameStr, password=dbPassStr)

    # get a cursor object from the connection
    cur = conn.cursor()

    # create sql command for rows delete
    sqlTxt = 'DELETE FROM public.students where name = %s'

    # execute the data delete SQL command along with the SQL placeholder values 
    cur.execute(sqlTxt, ("xyz",))

    rowCount = cur.rowcount
    print("number of deleted rows =", rowCount)

    # commit the changes
    conn.commit()
except (Exception, psycopg2.Error) as error:
    print("Error while interacting with PostgreSQL...\n", error)
finally:
    if(conn):
        # close the cursor object to avoid memory leaks
        cur.close()
        # close the connection object also
        conn.close()

print("data deletion example code execution complete...")
```

## Update rows example
```python
import psycopg2
import datetime as dt
import pandas as pd

hostStr = 'localhost'
dbPort = 5433
dbStr = 'test1'
uNameStr = 'postgres'
dbPassStr = 'pass'
# initialize the connection object
conn=None
try:
    conn = psycopg2.connect(host=hostStr, port=dbPort, dbname=dbStr,
                            user=uNameStr, password=dbPassStr)

    # get a cursor object from the connection
    cur = conn.cursor()

    # create sql command for rows update
    sqlTxt = 'UPDATE public.students set name = %s where name = %s'

    # execute the sql to perform insertion
    cur.execute(sqlTxt, ("hgf", "abc"))

    rowCount = cur.rowcount
    print("number of updated rows =", rowCount)

    # commit the changes
    conn.commit()
except (Exception, psycopg2.Error) as error:
    print("Error while interacting with PostgreSQL", error)
finally:
    if(conn):
        # close the cursor object to avoid memory leaks
        cur.close()
        # close the connection object also
        conn.close()

print("data update example code execution complete...")
```
### Video
The videos for this post can be found [here](https://youtu.be/p33XTKbFeBE) and [here](https://youtu.be/_AO5uMEEjfo)

<iframe width="560" height="315" src="https://www.youtube.com/embed/p33XTKbFeBE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/_AO5uMEEjfo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### References
* psycopg2 documentation - https://www.psycopg.org/docs/usage.html
* psycopg2 sql parameters documentation - https://www.psycopg.org/docs/usage.html#passing-parameters-to-sql-queries
* cursor rowcount variable documentation - https://www.psycopg.org/docs/cursor.html#cursor.rowcount 
* PostgreSQL Official docs - https://www.postgresql.org/docs/14/index.html
* pgAdmin download - https://www.pgadmin.org/download/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU1NTM2ODA3MiwxNDM4MjgzOTM5LC01NT
UzNjgwNzIsNzExOTQxOTI4LC01MDMwNTAwMjEsLTEwOTc4MTMx
MjMsLTE4Mjk5NjU1MjUsLTY5ODI5MDIwOCwxMjM2Mzk3MTk0LD
UwMjU3MzQ2MSwtNDEyMTU0MzYzLC04MTMzOTg0NzgsMTg2MDcx
NjI2NSw2OTgwOTY0NzMsNzUyMzkwNzQ1LDQwODE4MDc3LDE0ND
g0NjkxNCwtMTUzNjc2NzgzMiwtMjEzMTIxMTM3MCwyMDQ0ODUz
MTddfQ==
-->