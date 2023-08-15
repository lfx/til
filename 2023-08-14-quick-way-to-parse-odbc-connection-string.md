# Quick way to parse odbc connection string

```python
SQLSRV_CONNECTION="SERVER=tcp:127.0.0.1,1433;ENCRYPT=no;UID=sqlserver;PWD=secretP44sw0rd"
sp = SQLSRV_CONNECTION.split(";")
m1 = map(lambda x: x.split("="), sp)
d1 = dict(m1)
print(d1["PWD"])
```
