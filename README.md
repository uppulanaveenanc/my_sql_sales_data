# my_sql_sales_data
``` sql
select * from sales_data
```
``` sql	
select
count(*)
from sales_data
```

``` sql
delete from sales_data
where 
	transaction_id is NULL
	OR
	sale_date is NULL
	OR
	sale_time is NULL
	OR
	customer_id is NULL
	OR
	gender is NULL
	OR
	age is NULL
	OR
	category is NULL
	OR
	quantity is NULL
	OR
	price_per_unit is NULL
	OR
	cogs is NULL
	OR
	total_sale is NULL;
```
1. **write a sql query to fetch where the sale-date is '2022-11' and customer_id**
``` sql
	select * from sales_data
	where
		TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
		AND
		customer_id = 117
```
2 **Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17)**
``` sql
WITH hourly_sale
AS
(
SELECT *,
    CASE
        WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
        WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END as shift
FROM sales_data
)
SELECT 
    shift,
    COUNT(*) as total_orders    
FROM hourly_sale
GROUP BY shift
```

		
