# PySurrealDB
An unofficial library to connect to SurrealDB.

The official surreal library is only async, has a lot of dependancies, and is currently undocumented.

---
## Getting Started

If you don't already have it, install [SurrealDB](https://surrealdb.com/docs/start/installation)

Linux: 
``` bash
$ curl -sSf https://install.surrealdb.com | sh
# then
$ surreal start --user test --pass test
```


### Install PySurrealDB
PySurrealDB currently has no dependancies, so it can be used on its own by cloning the repo.



### Examples

```python
import pysurrealdb as surreal

conn = surreal.connect(user='test', password='test')

conn.create('person', {'name': 'Mike'})
conn.query('select * from person')
```

To connect to a live SurrealDB server, you can specify the connection info either in the connect call, or in a config file.

```python
import pysurrealdb as surreal
conn = surreal.connect(host='surreal.com', port=8000, user='user', password='pass', database='db', namespace='ns')
```

Optional Config file:
```python
# use a configured connection. 
conn = surreal.connection('default')
# Requires pysurrealdb.json file. Place it in your root directory, or specify the file location with the env variable 'PYSURREALDB_CONFIG'.

Example pysurrealdb.json:
{
    "connections": {
        "default": {
            "host": "localhost",
            "port": 8000,
            "user": "test",
            "password": "test"
            "database": "test",
            "namespace": "test",
        }
    }
}
```


## Query Builder

You can write queries using laravel and masonite style syntax:
```python
import pysurrealdb as surreal
conn = surreal.connection()

# setup data
conn.drop('person')
conn.insert('person', [{'name': 'Mike', 'age': 31}, {'name':'Mr P'}])

# query builder examples
first_person = conn.table('person').where('name', 'Mike').first()

adults = conn.table('person').where('age', '>=', 18).order_by('age', 'desc').limit(10).get()
```


This project is a work in progress. Please email aurelion314@gmail.com if you have any questions or feedback. Thanks!