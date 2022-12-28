# MySQL

## collection of facts

### default credentials
```
root : NOPASSWORD 		; if within rules of engagement try bruteforcing this
PORT : 3306
```


## injection - SQLi

### general concepts

User input is improperly handled, resulting in the SQL service interpreting unintended code. This can result in the SQL service interpreting arbitrary statements crafted by an attacker. 

Possible outcomes are

- complete disclosure of database contents
- some injection allows for revision of existing entires; update statements
- additions of new entires is also possible
- authentication bypass
- escalation of privilege (authenticate as high priv user)


### techniques

#### dealing with single line output

When using `group_concat()` to dump multiple lines at once, the funciton goes directly after `SELECT`. E.g.
```sql
SELECT group_concat( table1,table2,table3, ... ) FROM TABLE_NAME
```

### procedures

> development of these procedure sheets and surround information are intended to facilitate my mastery of the topics. 


#### enumerate SQL database via UNION injection

The following methodology was developed while participating in TryHackMe's Advent of Cyber 2022. The challenge room for Day 16 provided a friendly target to practice enumerating a `MySQL` database, ultimatly resulting in the weaponization of a SQL injection vulnerabliity. 


##### reverse engineer the hard coded SQL statement

We need to determine the number of columns in the SQL statement. To do this, we use a valid query that returns data. We then perform a `UNION` with increasingly more integers or `NULL`s. A mismatch in number of columns in the statement and number of `NULL`s provided yields no data or an error. A match in the two counts results in the expected return of the initial valid statement.

```txt
/webapp/elf.php?id=1%20union%20all%20select%201,2,3,4,5,6,7
```

> union all is identical to union, however it includes all duplicates.

We can now  invalidate our original query, but allow the `1,2,3,...` to persist. This displays which columns of the backend statement are being returned as outputs. For this particular lab, `3,4` are returned.   

```txt
/webapp/elf.php?id=-1%20union%20all%20select%201,2,3,4,5,6,7
```

We can now enumerate the databases conected to the service by enumerating the meta-tables.


##### enumerate databases and associated tables connected to the service

We can enumerate the databases attached to the service by performing queries on the `information_schema` meta-table. This table is guaranteed to be available in the `MySQL` database, it is necessary for functionality. 

The following statement was created by consulting the official `MySQL` documentation on the `information_schema` table.

```txt
/webapp/elf.php?id=-1%20union%20all%20select%201,2,table_schema,table_name,5,6,7%20from%20information_schema.tables%20where%20table_schema%20not%20like%20%27%schema%%27
```

- `information_schema.tables` contains rows of information on all tables attached to the service
- `table_schema` is the name of a database that is attached to the service
- `table_name` is the name of a given table
- a row with columns `table_schema` and `table_name` describes the mapping between tables and databases
- our final clause `WHERE table_schema NOT LIKE '%schema%'` is a luxury for the attacker. We are using it to supress all the meta-tables associated with the service.


##### enumerate columns present in a discovered table

Armed with information on which tables are associated with which databases, we can create targeted queries to harvest high value information. If sensitive information is inside the database we can yank all of it. For defenders, a `UNION` SQuLi injection attack is nearly the worst case scenario. The only thing worse would be an `UPDATE` vulnerability, potentially resulting in a mass destruction event. 

Not shown here, from enumerating databasesand tables, we now have knowledge of a table called `users` from the `logistics` database. Once again we use the meta-tables to get information about what columns exist in the `users` table. We query the `information_schema.columns` table in the following way

```txt
/webapp/elf.php?id=-1%20union%20all%20select%201,2,column_name,table_name,5,6,7%20from%20information_schema.columns%20where%20table_schema%20like%20%27%logistics%%27%20and%20table_name%20like%20%27%users%%27
```

- `information_schema.columns` contains all column information of databases associated to the service
- `column_name` is the name of a column
- `table_name` is the name of the table\
- a row with columns `column_name` and `table_name` describes the mapping between columns and tables. We now know which columns belong to the `users` table, our high value target
- our final clause `WHERE table_schema LIKE 'logistics' AND table_name LIKE 'users'` specifies that we are only interested in the rows associated with the `users` table from the `logistics` database. 
- the `AND table_name LIKE 'users'` section can be removed to see all table-column mappings of the `logistics` database

##### target aquired,  finalize weaponization of the exploit

The previous enumerations revealed that

- the `logistics` database is attached to the service
- the `logistics` database has a table called `users`
- the `users` table has columns `username,password` amoung some other valuable fields
- arbitrary `UNION` statements are possible, resulting in extraction of any and all data from the `logistics` database

The final query:

```txt
/webapp/elf.php?id=-1%20union%20all%20select%201,2,username,password,5,6,7%20from%20users
```

- dumps username password mappings stored in the `logisitcs` database
- `logistics` database is not explicitly listed. Only one database was attached to this service, so it defaults to `logistics`

> the SQLi vulnerability has been weaponized and delivered over the network. You can now move on to exploitation of the compromised target


##### references for development of this procedure

> the following links are replicated in the "external sources" section at the bottom of this page

- [MySQL | information_schema reference](https://dev.mysql.com/doc/refman/8.0/en/information-schema-general-table-reference.html)
- [MySQL | information_schema.tables table ](https://dev.mysql.com/doc/refman/8.0/en/information-schema-tables-table.html)
- [MySQL | information_schema.columns table](https://dev.mysql.com/doc/refman/8.0/en/information-schema-columns-table.html)
- [MySQL | NOT operator](https://www.techonthenet.com/mysql/not.php)
- [MySQL | LIKE operator](https://www.w3schools.com/mysql/mysql_like.asp)
- [Understanding How Prepared Statements Prevent SQLi](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)



### external sources

- [pentestmonkey SQLi cheatsheet](https://pentestmonkey.net/cheat-sheet/sql-injection/mysql-sql-injection-cheat-sheet)
- [MySQL | information_schema reference](https://dev.mysql.com/doc/refman/8.0/en/information-schema-general-table-reference.html)
- [MySQL | information_schema.tables table ](https://dev.mysql.com/doc/refman/8.0/en/information-schema-tables-table.html)
- [MySQL | information_schema.columns table](https://dev.mysql.com/doc/refman/8.0/en/information-schema-columns-table.html)
- [MySQL | NOT operator](https://www.techonthenet.com/mysql/not.php)
- [MySQL | LIKE operator](https://www.w3schools.com/mysql/mysql_like.asp)
- [Understanding How Prepared Statements Prevent SQLi](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)

