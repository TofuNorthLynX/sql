#

Task-00
```sql
SELECT id as object_id, name as object_name FROM person
UNION
SELECT id, pizza_name FROM menu
ORDER BY object_id, object_name
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/10951696-3649-4fa7-a021-a36652ee12de)

Task-01
```sql
(SELECT name as object_name FROM person ORDER BY name)
UNION ALL
(SELECT pizza_name FROM menu ORDER BY pizza_name)
; 
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/1a6bf3c2-e105-4c4b-bd4c-a03ea20e843e)

#17.01.24

Task-02
```sql
SELECT pizza_name FROM menu
INTERSECT
SELECT pizza_name FROM menu
ORDER BY pizza_name DESC
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/c21ec969-dbdc-483f-b0e7-873160898384)

Task-03
```sql
SELECT order_date as action_date, person_id FROM person_order
INTERSECT ALL
SELECT visit_date, person_id FROM person_visits
ORDER BY action_date, person_id DESC
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/a07726e2-8ccc-40b5-8c0b-3bb08ea453c9)

Task-04
```sql
SELECT person_id, order_date FROM person_order
WHERE order_date = '2022-01-07'
INTERSECT ALL
SELECT person_id, visit_date FROM person_visits
WHERE visit_date = '2022-01-07'
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/a3fb9adf-eb7f-4be2-9c6d-5258cab52777)

Task-05
```sql
SELECT person.id, person.name, age, gender, address, pizzeria.id, pizzeria.name, rating FROM person, pizzeria
ORDER BY person.id
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/43406559-6145-4bad-b491-74414dd5779b)

Task-06
```sql
SELECT order_date as action_date, p.name as person_name FROM person_order po
JOIN person p ON p.id = po.person_id
INTERSECT ALL
SELECT visit_date, p.name FROM person_visits pv
JOIN person p ON p.id = pv.person_id
ORDER BY action_date, person_name DESC
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/f4d2040b-4ed7-4325-8fc6-b4f4f638f96e)

Task-07
```sql
SELECT 
	po.order_date, 
	p.name || ' (age:' || p.age || ')' as person_infomation 
	FROM person_order po
JOIN person p ON p.id = po.person_id
ORDER BY order_date, person_infomation
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/e3ea79ee-2131-4628-9025-15587714796a)

Task-08
```sql
SELECT 
	po.order_date, 
	p.name || ' (age:' || p.age || ')' as person_infomation 
	FROM (SELECT order_date, person_id AS id FROM person_order) po
NATURAL JOIN person p
ORDER BY order_date, person_infomation
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/8987b9fd-4479-47d7-8e67-5551135ad0e7)

Task-09
```sql
SELECT name FROM pizzeria pi 
WHERE id NOT IN (SELECT pizzeria_id FROM person_visits)
;

SELECT name FROM pizzeria pi 
WHERE NOT EXISTS (SELECT pizzeria_id FROM person_visits
			  WHERE person_visits.pizzeria_id = pi.id)
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/a260aa14-3a2f-44a8-8ef3-795c51595bad)

Task-10
```sql
SELECT 
	p.name as person_name,
	m.pizza_name as pizza_name,
	pi.name as pizzeria_name
	FROM person_order po
	JOIN person p ON p.id = po.person_id
	JOIN menu m ON m.id = po.menu_id
	JOIN pizzeria pi ON pi.id = m.pizzeria_id
	ORDER BY person_name, pizza_name, pizzeria_name
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/fa6e7fc6-7ba9-4a77-9649-2fb9c7a24e7d)
