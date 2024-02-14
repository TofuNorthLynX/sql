1
```
WITH sumord AS(
	SELECT 
	o.customer_id, 
	o.quantity * p.price as order_sum
	FROM orders o
JOIN products p ON p.product_id = o.product_id
WHERE order_date BETWEEN '2024-01-13' AND '2024-02-13'
),
help AS(SELECT sumord.customer_id, SUM(order_sum) FROM sumord
GROUP BY 1)

SELECT c.first_name, c.last_name, h.sum FROM customers c
JOIN help h ON h.customer_id = c.customer_id 
ORDER BY sum DESC LIMIT 3
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/12f5c554-39e2-400f-b289-116e7bd0d0bd)

2
```sql

```

3
```sql
UPDATE products 
SET price = (price - (price * 10 / 100))
WHERE category = 'Clothes'
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/9eca08da-2e74-47ae-bede-af5f1a776984)
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/b8f4fe24-ea14-4ce5-bfca-06c7c5ace839)

4
```sql
WITH avgg AS(
	SELECT 
	p.category, 
	AVG(price)
	FROM products p
GROUP BY 1
),
minm AS(
	SELECT MAX(avgg.avg) 
	FROM avgg
UNION
SELECT MIN(avgg.avg) 
	FROM avgg
)

SELECT avgg.category, avgg.avg FROM avgg
JOIN minm ON minm.max = avgg.avg
ORDER BY avg DESC
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/b73f9023-9334-4347-93f8-7788e2d15b7e)

5
```sql

```
