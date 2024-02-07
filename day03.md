Task-01
```sql
SELECT m.pizza_name, m.price, piz.name as pizzeria_name, pv.visit_date FROM person_visits pv
JOIN pizzeria piz ON piz.id = pv.pizzeria_id
JOIN menu m ON m.pizzeria_id = piz.id
JOIN person p ON p.id = pv.person_id
WHERE p.name = 'Kate' AND m.price BETWEEN 800 AND 1000
ORDER BY m.pizza_name, m.price, pizzeria_name;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/59dbcb08-ba89-47f6-b638-7f1e83663db7)

Task-01
```sql
SELECT id FROM menu m
EXCEPT
SELECT DISTINCT menu_id from person_order po
ORDER BY 1;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/936b0f2e-4933-49d0-9efa-22959c7c3a90)

Task-02
```sql
WITH ids AS(
	SELECT id FROM menu m
	EXCEPT
	SELECT DISTINCT menu_id from person_order po
	ORDER BY 1
)
SELECT m.pizza_name, m.price, piz.name FROM ids
JOIN menu m ON m.id = ids.id
JOIN pizzeria piz ON piz.id = m.pizzeria_id
ORDER BY m.pizza_name, m.price;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/121f065f-f934-425b-9bd2-ce419d63801e)

Task-03
```sql
WITH female_ord AS (
	SELECT pi.name as pizzeria_name FROM person_order po
	JOIN menu m ON m.id = po.menu_id
	JOIN person p ON p.id = po.person_id
	JOIN pizzeria pi ON pi.id = m.pizzeria_id
	WHERE p.gender = 'female'
), male_ord AS (
	SELECT pi.name as pizzeria_name FROM person_order po
	JOIN menu m ON m.id = po.menu_id
	JOIN person p ON p.id = po.person_id
	JOIN pizzeria pi ON pi.id = m.pizzeria_id
	WHERE p.gender = 'male'
), res AS (
	(SELECT * FROM female_ord
	EXCEPT ALL
	SELECT * FROM male_ord)
	UNION ALL
	(SELECT * FROM male_ord
	EXCEPT ALL
	SELECT * FROM female_ord))

SELECT DISTINCT * FROM res
ORDER BY 1;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/c9062b5d-43e4-460a-bc5a-c8cf3072646b)

Task-04
```sql
WITH female_ord AS (
	SELECT pi.name FROM person_order po
	JOIN menu m ON m.id = po.menu_id
	JOIN person p ON p.id = po.person_id
	JOIN pizzeria pi ON pi.id = m.pizzeria_id
	WHERE p.gender = 'female'
), male_ord AS (
	SELECT pi.name FROM person_order po
	JOIN menu m ON m.id = po.menu_id
	JOIN person p ON p.id = po.person_id
	JOIN pizzeria pi ON pi.id = m.pizzeria_id
	WHERE p.gender = 'male'
)

(
	SELECT * FROM female_ord
	EXCEPT
	SELECT * FROM male_ord
)
UNION
(
	SELECT * FROM male_ord
	EXCEPT
	SELECT * FROM female_ord
)
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/1e16fd4b-d083-4488-a9fd-d1793d16f283)

Task-05
```sql
WITH vis AS (
	SELECT piz.name as pizzeria_name FROM person_visits pv
	JOIN pizzeria piz ON piz.id = pv.pizzeria_id
	JOIN person p ON p.id = pv.person_id
	WHERE p.name = 'Andrey'
), ord AS (
	SELECT piz.name as pizzeria_name FROM person_order po
	JOIN menu m ON m.id = po.menu_id
	JOIN pizzeria piz ON piz.id = m.pizzeria_id
	JOIN person p ON p.id = po.person_id
	WHERE p.name = 'Andrey'
)

SELECT DISTINCT * FROM vis
EXCEPT
SELECT DISTINCT * FROM ord
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/4f37950f-48fa-4019-98d0-bc4a5675b82c)

Task-06
```sql

```

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

Task-11
```sql

```

Task-12
```sql

```

Task-13
```sql

```
