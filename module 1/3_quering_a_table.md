# Querying a table
In the worksheet you can use below queries to execute. The syntax is your familiar SQL query syntax. Let's execute it and observe the output;

```SQL
SELECT COUNT(*) FROM tasty_bytes_sample_data.raw_pos.menu WHERE item_category = 'Snack' AND item_subcategory = 'Warm Option';

SELECT * FROM tasty_bytes_sample_data.raw_pos.menu;

SELECT item_subcategory, MAX(SALE_PRICE_USD) FROM tasty_bytes_sample_data.raw_pos.menu WHERE item_subcategory IN ('Warm Option', 'Cold Option', 'Hot Option') GROUP BY 1 ORDER BY 2 DESC;
```