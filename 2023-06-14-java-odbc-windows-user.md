# TIL, JDBC - SQL Server with Win auth

Setting JDBC connection with Windous Auth is simple, just need to pass Win user and flag `integratedSecurity=true` like this

```
jdbc:sqlserver://WIN_DOMAIN\win_user;serverName=10.10.10.64;portNumber=1433;databaseName=DB_NAME;integratedSecurity=true
```
and need tell Java where to load external libs:

```
-Djava.library.path=C:\java\libs\for\jdbc
```
The external libs has to have dll's in Windows to make it work - `mssql-jdbc_auth-xxx`. Those can come from [various sources](https://www.google.com/search?q=mssql-jdbc_auth).
