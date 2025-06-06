# Virtual Warehouse
Virtual warehouse in Snowflake is a compute resouce like CPU, RAM and temporary storage space. It is different from the general notion of warehous being a repository of integrated data.

## Create and Use Virtual Warehouse
There are two ways to create virtual warehous
1. ### Using UI
* Click on Admin -> Warehouses
* Click on "Warehouse" with "+" icon
* Provide a suitable name
* You can retain Type as Standard
* Choose Size as "Small" from the drop down instead of default "X-Small"

2. ### Using SQL Query
```SQL
USE WAREHOUSE warehouse_gilberto;
CREATE WAREHOUSE warehouse_dash;
SHOW WAREHOUSES;
```

## Optional Resource
This is not mandatory reading, but here's the code we'll run in the "Virtual Warehouses" videos. It may come in handy when you're doing the associated hands-on assignment.

```SQL
---> what menu items does the Freezing Point brand sell?
SELECT 
   menu_item_name
FROM tasty_bytes_sample_data.raw_pos.menu
WHERE truck_brand_name = 'Freezing Point';

---> what is the profit on Mango Sticky Rice?
SELECT 
   menu_item_name,
   (sale_price_usd - cost_of_goods_usd) AS profit_usd
FROM tasty_bytes_sample_data.raw_pos.menu
WHERE 1=1
AND truck_brand_name = 'Freezing Point'
AND menu_item_name = 'Mango Sticky Rice';

CREATE WAREHOUSE warehouse_dash;
CREATE WAREHOUSE warehouse_gilberto;

SHOW WAREHOUSES;

USE WAREHOUSE warehouse_gilberto;

---> set warehouse size to medium
ALTER WAREHOUSE warehouse_dash SET warehouse_size=MEDIUM;

USE WAREHOUSE warehouse_dash;

SELECT
    menu_item_name,
   (sale_price_usd - cost_of_goods_usd) AS profit_usd
FROM tasty_bytes_sample_data.raw_pos.menu
ORDER BY 2 DESC;

---> set warehouse size to xsmall
ALTER WAREHOUSE warehouse_dash SET warehouse_size=XSMALL;

---> drop warehouse
DROP WAREHOUSE warehouse_vino;

SHOW WAREHOUSES;

---> create a multi-cluster warehouse (max clusters = 3)
CREATE WAREHOUSE warehouse_vino MAX_CLUSTER_COUNT = 3;

SHOW WAREHOUSES;

---> set the auto_suspend and auto_resume parameters
ALTER WAREHOUSE warehouse_dash SET AUTO_SUSPEND = 180 AUTO_RESUME = FALSE;

SHOW WAREHOUSES;

```