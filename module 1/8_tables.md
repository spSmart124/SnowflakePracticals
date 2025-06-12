# Tables
## Introduction
As you may be familiar with table from your knowledge of other database flavours like Oracle, SQL Server, MySql etc, it is a combination of rows and columns. Under the hood, Snowflake does not store a table as big chunk of columns. It stores it as micro-partitions for better performance and storage efficiency. Micro-partitions will not be discussed in here

## Creating Table from UI
You can create a table from UI. To do that follow below steps.
1. Click on Data -> Databases
1. Click on your Database from the list of databases
1. Click on Schema
1. Click on Create -> Table -> Standard button
1. Specify the table in below syntax

```SQL
create or replace TABLE TEST_DATABASE.TEST_SCHEMA.TEST_TABLE (
	TEST_NUMBER NUMBER,
	TEST_VARCHAR VARCHAR,
	TEST_BOOLEAN BOOLEAN,
	TEST_DATE DATE,
	TEST_VARIANT VARIANT,
	TEST_GEOGRAPHY GEOGRAPHY
);
```

## Querying a Table
You can use below query to get know different SQL queries related to a table

```SQL
SELECT * FROM TEST_DATABASE.TEST_SCHEMA.TEST_TABLE;

---> insert a row into the table we just created
INSERT INTO TEST_DATABASE.TEST_SCHEMA.TEST_TABLE
  VALUES
  (28, 'ha!', True, '2024-01-01', NULL, NULL);

SELECT * FROM TEST_DATABASE.TEST_SCHEMA.TEST_TABLE;

---> drop the test table
DROP TABLE TEST_DATABASE.TEST_SCHEMA.TEST_TABLE;

---> see all tables in a particular schema
SHOW TABLES IN TEST_DATABASE.TEST_SCHEMA;

---> undrop the test table
UNDROP TABLE TEST_DATABASE.TEST_SCHEMA.TEST_TABLE;

SHOW TABLES IN TEST_DATABASE.TEST_SCHEMA;

SHOW TABLES;

---> see table storage metadata from the Snowflake database
SELECT * FROM SNOWFLAKE.ACCOUNT_USAGE.TABLE_STORAGE_METRICS;

SHOW TABLES;

---> here’s an example of table we created previously
CREATE TABLE tasty_bytes.raw_pos.order_detail 
(
    order_detail_id NUMBER(38,0),
    order_id NUMBER(38,0),
    menu_item_id NUMBER(38,0),
    discount_id VARCHAR(16777216),
    line_number NUMBER(38,0),
    quantity NUMBER(5,0),
    unit_price NUMBER(38,4),
    price NUMBER(38,4),
    order_item_discount_amount VARCHAR(16777216)
);

```