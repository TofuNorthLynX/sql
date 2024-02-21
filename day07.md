Task-00
```sql
SELECT pv.person_id, COUNT(pv.id) as count_of_visits 
FROM person_visits pv
GROUP BY 1
ORDER BY 2 DESC, 1;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/bbe83df7-c808-479a-95a1-5eacad1817e8)

Task-01
```sql
SELECT p.name, COUNT(pv.id) as count_of_visits 
FROM person_visits pv
JOIN person p ON p.id = pv.person_id
GROUP BY 1
ORDER BY 2 DESC, 1 LIMIT 4;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/8be209fe-9875-4699-a9a0-c17d19fe2703)

Task-02
```sql
WITH vis AS (
	SELECT piz.name, COUNT(pv.id), 'visit' as action_type
	FROM person_visits pv
	JOIN pizzeria piz ON piz.id = pv.pizzeria_id
	GROUP BY 1
	ORDER BY 2 DESC, 1 LIMIT 3
), 
ord AS (
	SELECT piz.name, COUNT(po.id), 'order' as action_type
	FROM person_order po
	JOIN menu m ON m.id = po.menu_id
	JOIN pizzeria piz ON piz.id = m.pizzeria_id
	GROUP BY 1
	ORDER BY 2 DESC, 1 LIMIT 3
)

SELECT * FROM vis
UNION ALL
SELECT * FROM ord
ORDER BY 3,  2 DESC;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/b2db6199-9970-4499-942a-e5240fe99039)

Task-03
```sql
WITH vis AS (
	SELECT piz.name, COUNT(pv.id)
	FROM person_visits pv
	JOIN pizzeria piz ON piz.id = pv.pizzeria_id
	GROUP BY 1
), 
ord AS (
	SELECT piz.name, COUNT(po.id)
	FROM person_order po
	JOIN menu m ON m.id = po.menu_id
	JOIN pizzeria piz ON piz.id = m.pizzeria_id
	GROUP BY 1
),
alll AS (
SELECT * FROM vis
UNION ALL
SELECT * FROM ord
)
SELECT a.name, SUM(a.count) as total_count 
FROM alll a
GROUP BY 1
ORDER BY 2 DESC, 1;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/4581907f-28d2-4110-9f85-f7811545904d)

Task-04
```sql
WITH vis AS (
	SELECT p.name, COUNT(pv.id) as count_of_visits 
	FROM person_visits pv
	JOIN person p ON p.id = pv.person_id
	GROUP BY 1
)
SELECT * FROM vis
WHERE count_of_visits > 2 -- у нас нет более 3 заказов, как надо по заданию :(
ORDER BY 2 DESC, 1
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/1e999e3c-472b-4f96-b9ca-c5f3a56549e3)

Task-05
```sql
SELECT DISTINCT p.name FROM person_order po
JOIN person p ON p.id = po.person_id
ORDER BY 1;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/555406ce-9335-468b-bf1c-1b69cba9fd6d)

Task-06
```sql
SELECT 
	piz.name, 
	COUNT(po.id) as count_of_orders, 
	ROUND(AVG(m.price)::numeric, 2) as average_price, 
	MAX(m.price) as max_price, 
	MIN(m.price) as min_price 
	FROM person_order po
JOIN menu m ON m.id = po.menu_id
JOIN pizzeria piz ON piz.id = m.pizzeria_id
GROUP BY 1
ORDER BY 1;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/9edf9505-68e8-4d38-97e4-b934d716f742)

Task-07
```sql
SELECT 
	ROUND(AVG(piz.rating)::numeric, 4) as global_rating
	FROM pizzeria piz
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/46e4ebf2-b498-450d-964a-55d331206f1a)

Task-08
```sql
SELECT p.address, piz.name, COUNT(po.id)
FROM person_order po
JOIN menu m ON m.id = po.menu_id
JOIN pizzeria piz ON piz.id = m.pizzeria_id
JOIN person p ON p.id = po.person_id
GROUP BY 1, 2
ORDER BY 1, 2;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/e6bc70fe-c178-462b-af74-b3e02cc09c55)

Task-09
```sql
WITH tab AS(
	SELECT 
	p.address,
	ROUND(MAX(p.age) - (MIN(p.age)/MAX(p.age))::numeric, 2) as formula,
	ROUND(AVG(p.age)::numeric, 2) as average
FROM person p
GROUP BY 1
ORDER BY 1, 2)

SELECT *, 
	CASE
		WHEN formula > average THEN 'True'
		WHEN formula < average THEN 'False'
	END
	FROM tab;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/69b918fb-9450-436d-8558-ac13e360a3db)
