
## What is SQLite database

-   SQLite database is a file based database
-   Just like a CSV, an SQLite database will be a single file (like `app.db`)
-   It does not need a separate database server. Applications can interface with the database file directly. Hence it is easily portable
-   SQLite databases are generally used in use cases where concurrency, high data exchange speed is not required.

## SQL to create a database table

```sql
CREATE TABLE persons (
	id INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
	name TEXT(300) NOT NULL,
	dob TIMESTAMP NOT NULL,
	phone TEXT,
    CONSTRAINT persons_name_IDX UNIQUE (name),
    CONSTRAINT persons_phone_IDX UNIQUE (phone)
);

```

## Create Table example

-   The SQL command to create the table is run using the `execute` method on the connection object.

```python
import sqlite3
conn = sqlite3.connect("app.db")
conn.execute("""
CREATE TABLE if not exists persons (
	id INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
	name TEXT(300) NOT NULL,
	dob TIMESTAMP NOT NULL,
	phone TEXT,
    CONSTRAINT persons_name_IDX UNIQUE (name),
    CONSTRAINT persons_phone_IDX UNIQUE (phone)
);
""")
conn.close()

```

## VS Code extension to view SQLite database

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/sqlite%20vscode%20extension.png?raw=true)

-   Use CTRL+SHIFT+P in VS code to run the command `SQLite: Open Database` and open an SQLite database file as shown below. Also SQL commands can be executed easily with the commands `SQLite: New Query` and `SQLite: Run Query`

![image.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/sqlite%20vscode%20extension%20demo.png?raw=true)

## Insert single row example

-   An SQL INSERT command can executed as shown below to insert rows into a table
-   The INSERT command would be like

```sql
INSERT INTO table_name (column1, column2, column3) VALUES (12, "TEST", 36);

```

-   The data for named parameters `:name, :dob, :phone` in the SQL is provided as a python dictionary `{"name":"John","dob": dt.datetime(2000,1,24),"phone":"9876543210"}`

```python
import sqlite3
import datetime as dt

conn = sqlite3.connect("app.db")

employee = {
    "name": "John",
    "dob": dt.datetime(2000,1,24),
    "phone": "9876543210"
}

res = conn.execute("""
INSERT INTO persons (name,dob,phone) VALUES (:name,:dob,:phone);
""",employee)

print(f"number of inserted rows = {res.rowcount}")

conn.commit()
conn.close()

```

## Insert multiple rows example

-   `executemany` can be used to run a single SQL INSERT command multiple times for each parameters dictionary as shown below. Instead of using for loop to insert each row, this approach is more efficient and quick

```python
import sqlite3
import datetime as dt

conn = sqlite3.connect("app.db")

employees = [
    {"name": "Bob", "dob": dt.datetime(1992, 1, 24), "phone": "9765432942"},
    {"name": "Peter", "dob": dt.datetime(1994, 2, 10), "phone": "9876543087"},
    {"name": "Mark", "dob": dt.datetime(1998, 6, 15), "phone": "9876321049"}
]

res = conn.executemany("""
INSERT INTO persons (name,dob,phone) VALUES (:name,:dob,:phone);
""", employees)

print(f"number of inserted rows = {res.rowcount}")

conn.commit()
conn.close()

```

-   This approach can be used for update and delete database operations also

## Read table rows example

-   The following example gets the columns name, dob and phone from the table “persons” with a condition that dob is less than 01-Jan-2000
-   The SELECT command would be like

```sql
SELECT column1, column2, column3 from table_name WHERE column1>10 AND column2="TEST";

```

```python
import sqlite3
import datetime as dt

conn = sqlite3.connect("app.db")
cur = conn.cursor()

sqlParams = {"dob": dt.datetime(2000, 1, 1)}
rowsCursor = cur.execute("""
SELECT id, name, dob, phone from persons where dob<:dob;
""", sqlParams)

for r in rowsCursor:
    print(f"ID = {r[0]}, Name = {r[1]}, DoB = {r[2]}, Phone = {r[3]}")

# get all rows into a list
# print(rowsCursor.fetchall())

# get the column names of the returned rows
# fetchedColumns = [x[0] for x in rowsCursor.description]
# print(fetchedColumns)

cur.close()
conn.close()

```

-   The cursor object contains the rows returned by the SQL SELECT statement
-   Each row is a python tuple like `(6, "Bob", dt.datetime(1992,1,24), "9765432942”)`
-   The cursor rows can be iterated with a for..in loop as shown below
-   All rows can be retrieved at once as a list of tuples by calling the `fetchall()` method on the cursor

## Update table rows example

-   The following example updates the name column of the rows with id = 1
-   The UPDATE command would be like

```sql
UPDATE table_name SET column1=value1, column2=value2 where column3="TEST";

```

```python
import sqlite3
import datetime as dt

conn = sqlite3.connect("app.db")

sqlParams = {"name": "John Doe", "id": 1}
res = conn.execute("""
UPDATE persons SET name=:name where id=:id;
""", sqlParams)

print(f"number of updated rows = {res.rowcount}")

conn.commit()
conn.close()

```

## Delete table rows example

-   The following example deletes the rows with dob greater than Jan 1st 2000
-   The DELETE command would be like

```sql
DELETE from table_name WHERE column1>10 AND column2<50;

```

```python
import sqlite3
import datetime as dt

conn = sqlite3.connect("app.db")

sqlParams = {"dob": dt.datetime(2000, 1, 1)}
res = conn.execute("""
DELETE from persons where dob>:dob;
""", sqlParams)

print(f"number of deleted rows = {res.rowcount}")

conn.commit()
conn.close()

```

## Transactions example

-   A transaction can be started by executing the “BEGIN” statement
-   A transaction can be rolled-back / aborted by executing the “ROLLBACK” statement
-   A transaction can be committed to the database by executing the “COMMIT” statement
-   The following example creates a transaction deletes a row but rolls back the transaction. Hence no rows are deleted in the table after the transaction

```python
import sqlite3
import datetime as dt

conn = sqlite3.connect("app.db")

conn.execute("BEGIN")

sqlParams = {"name": "John"}
res = conn.execute("""
DELETE from persons where name=:name;
""", sqlParams)

print(f"number of deleted rows = {res.rowcount}")

rowsCursor = conn.execute("SELECT * from persons")
print(rowsCursor.fetchall())

conn.rollback()

rowsCursor = conn.execute("SELECT * from persons")
print(rowsCursor.fetchall())

conn.close()

```

## References

-   sqlite3 python module docs - [https://docs.python.org/3/library/sqlite3.html](https://docs.python.org/3/library/sqlite3.html)
-   cursor CRUD operations in sqlite3 - [https://docs.python.org/3/library/sqlite3.html#sqlite3.Cursor.execute](https://docs.python.org/3/library/sqlite3.html#sqlite3.Cursor.execute)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDQyNzQxOTEyLDEyMzM2MjE1NTddfQ==
-->