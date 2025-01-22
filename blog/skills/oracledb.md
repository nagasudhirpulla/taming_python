# oracledb python module as cx_Oracle replacement
-   python-oracledb is the new python module for connecting with Oracle database in place of cx_Oracle. The new module is more efficient with better intellisense suggestions and descriptive error messages.
-   Database connectivity can be established directly from python without installing oracle client libraries. This is called thin mode. This makes installing the module very easy.
-   Advanced functionality can be enabled by using oracle client libraries. This is called thick mode.
-   python-oracledb can be used as it is like cx_Oracle. In fact, the following can be used in legacy code

```python
import oracledb as cx_Oracle
# ...
```

## Installing python-oracledb

-   Install the python-oracledb module using the following command

```bash
python -m pip install oracledb

```

## Connecting to Oracle

-   Connect to oracle using username, password, host IP or hostname, port, service name as shown below

```python
import oracledb
conn = oracledb.connect(user="hr", password="pwd",
                              host="localhost", port=1521, service_name="xepdb1")

```

## References

- Official tutorial - [https://oracle.github.io/python-oracledb/samples/tutorial/Python-and-Oracle-Database-The-New-Wave-of-Scripting.html](https://oracle.github.io/python-oracledb/samples/tutorial/Python-and-Oracle-Database-The-New-Wave-of-Scripting.html)
- Connect to database with oracledb - [https://python-oracledb.readthedocs.io/en/latest/user_guide/connection_handling.html](https://python-oracledb.readthedocs.io/en/latest/user_guide/connection_handling.html)
- Connection parameters - [https://python-oracledb.readthedocs.io/en/latest/api_manual/connect_params.html#connectparams-attributes](https://python-oracledb.readthedocs.io/en/latest/api_manual/connect_params.html#connectparams-attributes)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2OTcwMDE3MDYsLTU2MTIwMDA3OSwtMj
A4ODc0NjYxMl19
-->