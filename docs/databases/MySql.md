# MySQL

> defaults 
```
root : NOPASSWORD 		; if within rules of engagement try bruteforcing this
PORT : 3306
```


## injection - SQLi


### general concepts

User input is improperly handled, resulting in the SQL service interpreting unintended code. This can result in the SQL service interpreting arbitrary statements crafted by an attacker. 

This can result in

- complete disclosure of database contents
- some injection allows for revision of existing entires 
- additions of new entires is also possible


### techniques

When using `group_concat()` to dump multiple lines at once, the funciton goes directly after `SELECT`. E.g.
```sql
SELECT group_concat( table1,table2,table3, ... ) FROM TABLE_NAME
```


### external sources

- [pentestmonkey SQLi cheatsheet](https://pentestmonkey.net/cheat-sheet/sql-injection/mysql-sql-injection-cheat-sheet)
