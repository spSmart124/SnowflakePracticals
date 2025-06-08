# Databases and Schemas
## Introduction
A database in a container for schemas. A schema is a container of objects like tables, views etc. Database and schema act as folders for different objects to put it in a simple way.

## Snowflake DB setup
Snowflake provides a default database called Snowflake. It contains a bunch of schemas like account_usage and alert etc. The database provides observability for the snowflake account. User created tables has two default schemas public and information_schema. information_schema contains different views like "TABLES", "STAGES" etc. to provide details about the different objects present in different other user created schemas. For example you can find out all the tables in a database by querying the information_schema's TABLES view.

```SQL
SELECT * FROM TASTY_BYTES.INFORMATION_SCHEMA.TABLES LIMIT 10;
```

## Database Commands
Here are the different commands to work with databases.
* Creating a database
___ Syntax: ___
```SQL
CREATE DATABASE <database_name>;
```

___ Exampe: ___
```SQL
CREATE DATABASE test_database;
```

* List database
___ Exampe: ___
```SQL
SHOW DATABASES;
```

* Drop a database
___ Syntax: ___
```SQL
DROP DATABASE <database_name>;
```

___ Exampe: ___
```SQL
DROP DATABASE test_database;
```

* Undrop a database
___ Syntax: ___
```SQL
UNDROP DATABASE <database_name>;
```

___ Exampe: ___
```SQL
UNDROP DATABASE test_database;
```

## Schema Commands
Here are the different commands to work with schemas which are very similar to those used for databases.
* Creating a schema
___ Syntax: ___
```SQL
CREATE SCHEMA <schema_name>;
```

___ Exampe: ___
```SQL
CREATE SCHEMA test_schema;
```

* List schema
___ Exampe: ___
```SQL
SHOW SCHEMAS;
```

* Drop a schema
___ Syntax: ___
```SQL
DROP SCHEMA <schema_name>;
```

___ Exampe: ___
```SQL
DROP SCHEMA test_schema;
```

* Undrop a database
___ Syntax: ___
```SQL
UNDROP SCHEMA <schema_name>;
```

___ Exampe: ___
```SQL
UNDROP SCHEMA test_schema;
```
