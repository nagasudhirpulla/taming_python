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
    conn = psycopg2.connect(host=hostStr, port=dbPort, dbname=dbStr,
                            user=uNameStr, password=dbPassStr)

    # get a cursor object from the connection
    cur = conn.cursor()

    # do something like fetch rows, insert rows, update rows, delete rows ...
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
* In the above program, we use 2 objects called connection object and cursor object
* Connection object establishes connection with the database
* Cursor object uses the connection object to fetch data from the database or update data in the database

### References
* psycopg2 documentation - https://www.psycopg.org/docs/usage.html
* PostgreSQL Official docs - https://www.postgresql.org/docs/14/index.html
* pgAdmin download - https://www.pgadmin.org/download/

<hr/>

[Table of Contents](https://nagasudhir.blogspot.com/2020/04/taming-python-table-of-contents.html)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4ODEyMDM4MzYsMTk3OTg4MTM2MCwtMT
M2NDI1MTQyOSwxMDI3MTIwMjI0LC0xMTUzNjcxNTgyXX0=
-->