# Semi Structured Data

## Introduction
Data can be of different types. Like structure, semi structured and unstructured data. Structured data like data in a row and column format. Semi structured data is data like JSON, XML, AVRO etc. which has some sort of structure. Unstructured data is data in an image or a text.

Snowflake provides VARIANT data type to allow semistructured data to be stored. VARIANT is a really flexible data type. It can hold any other type of data. Snowflake keeps track of actual datatype of the data stored in a VARIANT datatype column. For example, you can store a number on VARIANT datatype column and perform some numeric operations.

```SQL
---> create the test_menu table with just a variant column in it, as a test
CREATE TABLE tasty_bytes.RAW_POS.TEST_MENU (cost_of_goods_variant)
AS SELECT cost_of_goods_usd::VARIANT
FROM tasty_bytes.RAW_POS.MENU;

---> notice that the column is of the VARIANT type
DESCRIBE TABLE tasty_bytes.RAW_POS.TEST_MENU;

---> but the typeof() function reveals the underlying data type
SELECT TYPEOF(cost_of_goods_variant) FROM tasty_bytes.raw_pos.test_menu;

---> Snowflake lets you perform operations based on the underlying data type
SELECT cost_of_goods_variant, cost_of_goods_variant*2.0 FROM tasty_bytes.raw_pos.test_menu;
```

## OBJECT datatype
JSON in a VARIANT datatype column is stored as OBJECT data type. You can check the datatype as you have seen before using TYPEOF() function. typeof JSON data in Snowflake is OBJECT. you can think of OBJECT datatype as something that stores value in key value pair. So, you can perform some operation on OBJECT data type column to fetch value directly using colon (:) or square bracket ([]) syntax. Refer to below examples.

```SQL
---> you can use the colon to pull out info from menu_item_health_metrics_obj
SELECT MENU_ITEM_HEALTH_METRICS_OBJ:menu_item_health_metrics FROM tasty_bytes.raw_pos.menu;

---> use typeof() to see the underlying type
SELECT TYPEOF(MENU_ITEM_HEALTH_METRICS_OBJ) FROM tasty_bytes.raw_pos.menu;

SELECT MENU_ITEM_HEALTH_METRICS_OBJ, MENU_ITEM_HEALTH_METRICS_OBJ['menu_item_id'] FROM tasty_bytes.raw_pos.menu;
```

## ARRAY datatype
This type of data contains an Array in VARIANT datatype column value. Array is similar to array in programming where there will be one or more items on it and it can be accessed using index. 0 for the first item, 1 for the second item and so on.

## LATERAL FLATEN table function
Below example will demonstrate how can extract values from colon (:) notation and bracket notation for OBJECT data type. There is a function to make this job easier and simple. The function is LATERAL FLATEN(). Below demonstration shows how it can be achieved.


```SQL
CREATE TABLE TASTY_BYTES.RAW_POS.TEST_MENU1 (ingredients)
AS SELECT MENU_ITEM_HEALTH_METRICS_OBJ
FROM TASTY_BYTES.RAW_POS.MENU;

SELECT * FROM TASTY_BYTES.RAW_POS.TEST_MENU1;

DESCRIBE TABLE TASTY_BYTES.RAW_POS.TEST_MENU1;

SELECT TYPEOF(ingredients) FROM TASTY_BYTES.RAW_POS.TEST_MENU1;

CREATE TABLE TASTY_BYTES.RAW_POS.TEST_MENU2 (ingredients)
AS SELECT MENU_ITEM_HEALTH_METRICS_OBJ['menu_item_health_metrics']
FROM TASTY_BYTES.RAW_POS.MENU;

SELECT * FROM TASTY_BYTES.RAW_POS.TEST_MENU2;

SELECT TYPEOF(ingredients) FROM TASTY_BYTES.RAW_POS.TEST_MENU2;

CREATE TABLE TASTY_BYTES.RAW_POS.TEST_MENU3 (ingredients)
AS SELECT MENU_ITEM_HEALTH_METRICS_OBJ['menu_item_health_metrics'][0]
FROM TASTY_BYTES.RAW_POS.MENU;

SELECT * FROM TASTY_BYTES.RAW_POS.TEST_MENU3;

SELECT TYPEOF(ingredients) FROM TASTY_BYTES.RAW_POS.TEST_MENU3;

CREATE TABLE TASTY_BYTES.RAW_POS.TEST_MENU4 (ingredients)
AS SELECT MENU_ITEM_HEALTH_METRICS_OBJ['menu_item_health_metrics'][0]['ingredients']
FROM TASTY_BYTES.RAW_POS.MENU;

SELECT TYPEOF(ingredients) FROM TASTY_BYTES.RAW_POS.TEST_MENU4;

CREATE TABLE TASTY_BYTES.RAW_POS.TEST_MENU5 (ingredients)
AS SELECT MENU_ITEM_HEALTH_METRICS_OBJ['menu_item_health_metrics'][0]['ingredients'][0]
FROM TASTY_BYTES.RAW_POS.MENU;

SELECT * FROM TASTY_BYTES.RAW_POS.TEST_MENU5;

SELECT TYPEOF(ingredients) FROM TASTY_BYTES.RAW_POS.TEST_MENU5;

-- LATERAL FLATEN
SELECT
*
FROM TASTY_BYTES.RAW_POS.menu m,
LATERAL FLATTEN(input => m.menu_item_health_metrics_obj:menu_item_health_metrics);

SELECT
m.menu_item_name,
value:ingredients[0] AS ingredients
FROM TASTY_BYTES.RAW_POS.menu m,
LATERAL FLATTEN(input => m.menu_item_health_metrics_obj:menu_item_health_metrics);

CREATE OR REPLACE VIEW TASTY_BYTES.ANALYTICS.menu_v
AS
SELECT
m.menu_item_health_metrics_obj:menu_item_id::INTEGER AS menu_item_id,
value:is_healthy_flag::VARCHAR(1) AS is_healthy_flag,
value:is_gluten_free_flag::VARCHAR(1) AS is_gluten_free_flag,
value:is_dairy_free_flag::VARCHAR(1) AS is_dairy_free_flag,
value:is_nut_free_flag::VARCHAR(1) AS is_nut_free_flag
FROM TASTY_BYTES.RAW_POS.menu m,
LATERAL FLATTEN(input => m.menu_item_health_metrics_obj:menu_item_health_metrics);

SELECT
COUNT(DISTINCT menu_item_id) AS total_menu_items,
SUM(CASE WHEN is_healthy_flag = 'Y' THEN 1 ELSE 0 END) AS healthy_item_count,
SUM(CASE WHEN is_gluten_free_flag = 'Y' THEN 1 ELSE 0 END) AS gluten_free_item_count,
SUM(CASE WHEN is_dairy_free_flag = 'Y' THEN 1 ELSE 0 END) AS dairy_free_item_count,
SUM(CASE WHEN is_nut_free_flag = 'Y' THEN 1 ELSE 0 END) AS nut_free_item_count
FROM TASTY_BYTES.ANALYTICS.menu_v;
```