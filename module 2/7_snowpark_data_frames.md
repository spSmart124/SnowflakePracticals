# Snowpark Dataframes
Snowpark data frames are non-sql worksheets like python, java, scala etc. Wheneven you would like to use any non-sql language to perform data analysis you can use snowpark. Data Engineering has 3 parts
1. Ingestion
1. Transformation
1. Delivery

Snowpark comes in the transformation category.


## Query a table and show results.

```python
# import what you need
import snowflake.snowpark as snowpark

# import col
#from snowflake.snowpark.functions import col

# make sure to define main when you’re working in a Python worksheet
def main(session: snowpark.Session): 

    # load your table as a dataframe
    df_table = session.table("TASTY_BYTES.RAW_POS.MENU")

    # execute the operations. (Remember, Snowpark DataFrames are evaluated lazily.)
    df_table.show()

    # return your table
    return df_table
```

## Query a table using SELECT statement

```python
# import what you need
import snowflake.snowpark as snowpark

# import col
from snowflake.snowpark.functions import col

# make sure to define main when you’re working in a Python worksheet
def main(session: snowpark.Session): 

    # load your table as a dataframe
    df_table = session.table("TASTY_BYTES.RAW_POS.MENU")

    # execute the operations. (Remember, Snowpark DataFrames are evaluated lazily.)
    df_table.show()

    # load data using a query through session.sql instead of through session.table
    df_table2 = session.sql("SELECT * FROM TASTY_BYTES.RAW_POS.MENU LIMIT 5")

    # return your table
    return df_table2
```

## Filter Data


```python
# import what you need
import snowflake.snowpark as snowpark

# import col
from snowflake.snowpark.functions import col

# make sure to define main when you’re working in a Python worksheet
def main(session: snowpark.Session): 

    # load your table as a dataframe
    df_table = session.table("TASTY_BYTES.RAW_POS.MENU")

    # filter rows
    df_table = df_table.filter(col("TRUCK_BRAND_NAME") == "Freezing Point")

    # execute the operations. (Remember, Snowpark DataFrames are evaluated lazily.)
    df_table.show()

    # return your table
    return df_table

```

## Select columns

```python
# import what you need
import snowflake.snowpark as snowpark

# import col
from snowflake.snowpark.functions import col

# make sure to define main when you’re working in a Python worksheet
def main(session: snowpark.Session): 

    # load your table as a dataframe
    df_table = session.table("TASTY_BYTES.RAW_POS.MENU")

    # select columns
    df_table = df_table.select(col("MENU_ITEM_NAME"), col("ITEM_CATEGORY"))

    # execute the operations. (Remember, Snowpark DataFrames are evaluated lazily.)
    df_table.show()

    # return your table
    return df_table

```

## Chaining in snowpark

```python
# import what you need
import snowflake.snowpark as snowpark

# import col
from snowflake.snowpark.functions import col

# make sure to define main when you’re working in a Python worksheet
def main(session: snowpark.Session): 

    # load your table as a dataframe
    df_table = session.table("TASTY_BYTES.RAW_POS.MENU")

# filter and select at the same time (chaining)
    df_table = df_table.filter(
       col("TRUCK_BRAND_NAME") == "Freezing Point"
    ).select(
       col("MENU_ITEM_NAME"), 
       col("ITEM_CATEGORY")
    )

    # execute the operations. (Remember, Snowpark DataFrames are evaluated lazily.)
    df_table.show()

    # return your table
    return df_table

```

## Write result to a table


```python
# import what you need
import snowflake.snowpark as snowpark

# import col
from snowflake.snowpark.functions import col

# make sure to define main when you’re working in a Python worksheet
def main(session: snowpark.Session): 

    # load your table as a dataframe
    df_table = session.table("TASTY_BYTES.RAW_POS.MENU")

# filter and select at the same time (chaining)
    df_table = df_table.filter(
       col("TRUCK_BRAND_NAME") == "Freezing Point"
    ).select(
       col("MENU_ITEM_NAME"), 
       col("ITEM_CATEGORY")
    )

    # execute the operations. (Remember, Snowpark DataFrames are evaluated lazily.)
    df_table.show()

    # save your dataframe as a table!
    df_table.write.save_as_table("TEST_DATABASE.TEST_SCHEMA.FREEZING_POINT_ITEMS", mode="append")

    # return your table
    return df_table

```