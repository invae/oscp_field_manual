# NoSQL_MongoDB

"not-only-SQL" allows for data to be stored in creative ways. 


## basic CLI movements

> list databases connected to service
```bash
show dbs
```


> use a database 
```bash
use NAME_OF_DB
```


> list what is in the database
```bash
show collections
```


>dump data from collection via `find()` method
```bash
db.COLLECTION_NAME.find()
```


## techniques

### auth bypass via tautology

Always true statements can be used to bypass authentication. In this case, boolean OR.
```SQL
' || '1=1
```