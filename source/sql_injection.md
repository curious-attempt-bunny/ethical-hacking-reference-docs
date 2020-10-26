# SQL Injection

http://pentestmonkey.net/cheat-sheet/sql-injection/mysql-sql-injection-cheat-sheet
```
SELECT host, user, password FROM mysql.users -- 
```

## MySQL queries

```
SELECT table_schema,table_name FROM information_schema.tables WHERE table_schema <> 'mysql' AND table_schema <> 'information_schema';
```
