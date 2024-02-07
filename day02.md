Task-00
```sql
SELECT p.name, p.rating FROM pizzeria p
LEFT JOIN person_visits pv ON p.id = pv.pizzeria_id
WHERE pv.id IS NULL
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/ab483941-0b33-470e-907b-1d8604803f6d)

Task-01
```sql
SELECT days::date FROM generate_series('2022-01-01', '2022-01-10', interval '1 day') AS days
LEFT JOIN
		(SELECT missing_days::date AS missing_day, pv.visit_date FROM generate_series('2022-01-01', '2022-01-10', interval '1 day') AS missing_days
		JOIN person_visits pv ON pv.visit_date = missing_days.missing_days
		WHERE pv.person_id = 1 OR pv.person_id = 2) AS tab
	ON days.days = tab.visit_date
WHERE tab.visit_date IS NULL
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/964b807d-a429-45bb-aeec-11fd8e70df27)

Task-02
```sql
SELECT 
	COALESCE(p.name, '-') as person_name,
	pv.visit_date, 
	COALESCE(pi.name, '-') as pizzeria_name
	FROM person p
LEFT JOIN person_visits pv ON p.id = pv.person_id AND pv.visit_date BETWEEN '2022-01-01' AND '2022-01-03'
FULL JOIN pizzeria pi ON pi.id = pv.pizzeria_id
ORDER BY 1, 2, 3
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/40d8cbdf-fe29-4181-90cb-0439b04339ba)

Task-03
```sql
WITH daay AS (SELECT days::date FROM generate_series('2022-01-01', '2022-01-10', interval '1 day') AS days
	LEFT JOIN
			(SELECT missing_days::date AS missing_day, pv.visit_date FROM generate_series('2022-01-01', '2022-01-10', interval '1 day') AS missing_days
			JOIN person_visits pv ON pv.visit_date = missing_days.missing_days
			WHERE pv.person_id = 1 OR pv.person_id = 2) AS tab
		ON days.days = tab.visit_date
	WHERE tab.visit_date IS NULL)
SELECT * FROM daay;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/4e18c5bf-202b-4d4f-ab80-b8f7f2f787a4)

Task-04
```sql
SELECT m.pizza_name, pi.name, m.price FROM menu m
JOIN pizzeria pi ON m.pizzeria_id = pi.id
WHERE m.pizza_name = 'mushroom pizza' OR m.pizza_name = 'pepperoni pizza'
ORDER BY 1, 2
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/2525fc05-c7e8-4e8e-a6cc-771122571afa)

Task-05
```sql
SELECT p.name FROM person p
WHERE age > 25 AND gender = 'female'
ORDER BY p.name
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/ae6deeb5-6159-4293-a2c4-55e981aba61a)

Task-06
```sql
WITH tab as(
	SELECT pizza_name, pz.name as pizzeria_name, p.name FROM menu m
	JOIN pizzeria pz ON m.pizzeria_id = pz.id
	JOIN person_order po ON po.menu_id = m.id
	JOIN person p ON po.person_id = p.id
)

SELECT pizza_name, pizzeria_name FROM tab
WHERE tab.name = 'Anna' OR tab.name = 'Denis'
ORDER BY 1;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/38e02b1f-dc23-467e-a05b-acdece306068)

Task-07
```sql
SELECT 
	pz.name AS pizzeria_name,
	p.name AS person_name,
	m.price,
	pv.visit_date
FROM
	person_visits pv
JOIN person p ON pv.person_id = p.id 
JOIN person_order po ON po.order_date = pv.visit_date
JOIN menu m ON po.menu_id = m.id
JOIN pizzeria pz ON pz.id = pv.pizzeria_id
WHERE 
	visit_date = '2022-01-8'
	AND p.name = 'Dmitriy'
	AND m.price <= 800;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/f286678e-2f06-4a7d-b49c-d79ae9568385)

Task-08
```sql
SELECT p.name FROM person p
JOIN person_order po ON p.id = po.person_id 
JOIN menu m ON m.id = po.menu_id
WHERE (
		p.address = 'Moscow' OR
		p.address = 'Samara'
	) AND (
		m.pizza_name = 'mushroom pizza' OR
		m.pizza_name = 'pepperoni pizza'
	) AND p.gender = 'male'
ORDER BY 1 DESC;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/c7edcbbf-a1f5-43d2-80a5-6aed341a7b3b)

Task-09
```sql
SELECT p.name FROM person p
JOIN person_order po ON p.id = po.person_id 
JOIN menu m ON m.id = po.menu_id
WHERE (
		m.pizza_name = 'cheese pizza' OR
		m.pizza_name = 'pepperoni pizza'
	) AND p.gender = 'female'
ORDER BY 1;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/c3b4f29b-2dff-4955-b626-5d5bb51a2b9b)

Task-10
```sql
SELECT p1.name, p2.name, p1.address FROM person p1
JOIN person p2 ON p1.address = p2.address
WHERE p2.name > p1.name
ORDER BY 1, 2, 3;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/698d3f6a-4197-44ba-9721-1f0fe856a7eb)
