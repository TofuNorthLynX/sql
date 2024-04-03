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
WITH pizza_s AS (
	SELECT m1.pizza_name, m1.pizzeria_id as pi_1, m2.pizzeria_id as pi_2, m1.price FROM menu m1
	JOIN menu m2 ON m1.pizza_name = m2.pizza_name AND m1.price = m2.price AND m1.pizzeria_id > m2.pizzeria_id
)

SELECT pizza_name, pi1.name, pi2.name, price FROM pizza_s
JOIN pizzeria pi1 ON pi_1 = pi1.id
JOIN pizzeria pi2 ON pi_2 = pi2.id
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/24d17b0e-29a8-4530-94e4-70d5aaa9b375)

Task-07
```sql
INSERT INTO menu VALUES(19, 2, 'greek pizza', 800)
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/1fe0919e-da3a-4997-85dc-3c63664a5a8a)

Task-08
```sql
INSERT INTO menu VALUES(
	(SELECT MAX(id) FROM menu) +1, 
	(SELECT id FROM pizzeria
	WHERE name = 'Dominos'), 
	'sicilian pizza', 900)
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/89f8dbd7-0402-4c3c-90cf-978f67add696)

Task-09
```sql
INSERT INTO person_visits VALUES(
	(SELECT MAX(id) FROM person_visits) +1,
	(SELECT id FROM person
	WHERE name = 'Denis'),
	(SELECT id FROM pizzeria
	WHERE name = 'Dominos'), 
	'2022-02-24'),
	((SELECT MAX(id) FROM person_visits) +2, 
	(SELECT id FROM person
	WHERE name = 'Irina'),
	(SELECT id FROM pizzeria
	WHERE name = 'Dominos'), 
	'2022-02-24')
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/95095131-e28c-4d33-bd8c-0fa1554cd127)

Task-10
```sql
INSERT INTO person_order VALUES(
	(SELECT MAX(id) FROM person_order) +1,
	(SELECT id FROM person
	WHERE name = 'Denis'),
	(SELECT id FROM menu
	WHERE pizza_name = 'sicilian pizza'), 
	'2022-02-24'),
	((SELECT MAX(id) FROM person_order) +2, 
	(SELECT id FROM person
	WHERE name = 'Irina'),
	(SELECT id FROM menu
	WHERE pizza_name = 'sicilian pizza'), 
	'2022-02-24')
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/2510482a-9e77-454e-9aac-e08a04e4aa50)

Task-11
```sql
UPDATE menu
SET price = (800 - (800 * 10 / 100))
WHERE pizza_name = 'greek pizza';
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/a8bdcbcd-bb1d-4160-b3ec-786e8afacabf)

Task-12
```sql
INSERT INTO person_order(id, person_id, menu_id, order_date)
SELECT
	generate_series((SELECT MAX(id) FROM person_order) + 1,
			(SELECT MAX(id) FROM person) + 
			(SELECT MAX(id) FROM person_order), 
			1),
	generate_series((SELECT MIN(id) FROM person), 
			(SELECT MAX(id) FROM person)), 
			(SELECT id FROM menu 
			WHERE pizza_name = 'greek pizza'), 
			'2022-02-25';
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/7f744077-cc37-4fb2-aed0-93fe08b112f9)

Task-13
```sql
DELETE FROM person_order
WHERE order_date='2022-02-25';

DELETE FROM menu
WHERE pizza_name='greek pizza';
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/46e0fe13-3cc2-4687-8355-5f27a68b06c1)
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/5d72f255-09ea-43bb-8906-3d8bacf6b734)
