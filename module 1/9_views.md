# Views

## Introduction
Views are saved queries. When a query is executed that involves a view it executes the underlying query on the view. Views are of two types.

1. Non Materialized View
1. Materialized View

## Non Materialized View
Simple views are non materialized view. This type of view acts as a saved query and does not store the data in the database physically. Query involving non materialized view runs slower than materialized view as it has to execute the underlying query before it can provide the data

## Materialized View
Materialized view stores data physically in the database. Query involving materialized view runs faster than non materialized view as the data is fetched directly from the stored data. However, it comes with a cost that materialized view gets refreshed each time data is changed in the original table

## Creating and managing Views
You can use below syntax to work with views. Similar syntax is also applicable to materialized view. View does not support UNDROP command.

```SQL

-- Syntax
-- CREATE VIEW <database_name>.<schema_name>.<view_name>
-- AS
-- <Query>;

CREATE VIEW tasty_bytes.harmonized.brand_name
AS
SELECT truck_brand_names
FROM tasty_bytes.raw_pos.menu;

SHOW VIEWS;

DESCRIBE VIEW tasty_bytes.harmonized.brand_name;

-- ALTER VIEW

-- DROP VIEW
```

## Creating and managing Materialized Views
For the sake of completeness her is the example of the commands for materialized views.

```SQL

-- Syntax
-- CREATE MATERIALIZED VIEW <database_name>.<schema_name>.<view_name>
-- AS
-- <Query>;

CREATE MATERIALIZED VIEW tasty_bytes.harmonized.brand_name_materialized
AS
SELECT truck_brand_names
FROM tasty_bytes.raw_pos.menu;

SHOW VIEWS;

SHOW MATERIALIZED VIEWS;

DESCRIBE VIEW tasty_bytes.harmonized.brand_name;

DESCRIBE MATERIALIZED VIEW tasty_bytes.harmonized.brand_name;

-- ALTER MATERIALIZED VIEW

-- DROP MATERIALIZED VIEW
```