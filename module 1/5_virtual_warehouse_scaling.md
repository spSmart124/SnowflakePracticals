# Viratual Warehouse Scaling
There are two ways here
1. Vertical Scaling
1. Horizontal Scaling

## Vertical Scaling
In vertical scaling the warehouse computation size is altered between X-Small, Small, Medium till 6XL. There are two ways here.
1. ### Using Snowsite UI
* Click on Admin -> Warehouses
* Click on the Action button (... 3 dots) in the warehouse name row
* Click on Edit
* Change the Size from "X-Small" to "Small"
* Click on "Save Warehouse"

2. ### Using SQL Query
In the SQL worksheet you can use below queries.

```SQL
ALTER WAREHOUSE warehouse_dash SET warehouse_size='MEDIUM';
USE WAREHOUSE warehouse_dash;
SELECT * FROM tasty_bytes_sample_data.raw_pos.menu;
ALTER WAREHOUSE warehouse_dash SET warehouse_size='SMALL';
```

## Horizontal Scaling
In the approach of scaling more clusters are added to a warehouse to increase computation requirement instead to increasing the computation size. It is useful when the same warehouse runs multiple queries parallelly.

There are two ways here too.
1. ### Using Snowsite UI
* Click on Admin -> Warehouses
* Click on the Action button (... 3 dots) in the warehouse name row
* Click on Edit
* Expand the Advanced Option
* Check the "Multi-cluster Warehouse" checkbox
* Retain "Min Clusters" as 1
* Set "Max Clusters" to 3 or any appropriate value
* Click on "Save Warehouse"

2. ### Using SQL Query
In the SQL worksheet you can use below queries.

```SQL
DROP WAREHOUSE warehouse_vino;

CREATE WAREHOUSE warehouse_vino MAX_CLUSTER_COUNT = 3;

SHOW WAREHOUSES;

ALTER WAREHOUSE warehouse_vino SET AUTO_RESUME = FALSE AUTO_SUSPEND = 180;

SHOW WAREHOUSES;

ALTER WAREHOUSE warehouse_vino SUSPEND;
```