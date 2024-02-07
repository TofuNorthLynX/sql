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

```

Task-08
```sql

```

Task-09
```sql

```

Task-10
```sql

```
