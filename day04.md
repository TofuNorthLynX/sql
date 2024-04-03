Task-00
```sql
CREATE VIEW v_persons_male AS (
	SELECT * FROM person
	WHERE gender = 'male'
);
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/be4d16a7-7422-4cb9-8478-f75dcfb84cd6)

```sql
CREATE VIEW v_persons_female AS (
	SELECT * FROM person
	WHERE gender = 'female'
);
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/0a3187b7-0699-4390-85a1-2fb8981493e4)


Task-01
```sql
SELECT name FROM v_persons_male
UNION ALL
SELECT name FROM v_persons_female
ORDER BY name;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/b0f821e5-c4d4-48d3-ab28-fdfc1e10e931)

Task-02
```sql
CREATE VIEW v_generated_dates AS (
	SELECT all_dates::date as generated_date
	FROM generate_series('2022-01-01', '2022-01-31', interval '1 day') AS all_dates
);
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/19ddb08f-2b1e-49ca-8267-989c9f786a85)
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/53d4b1d1-c14c-4daf-8c07-1d359d80fbaa)

Task-03
```sql
SELECT generated_date as missing_date FROM v_generated_dates
EXCEPT
SELECT DISTINCT(visit_date) FROM person_visits 
	WHERE visit_date BETWEEN '2022-01-01' AND '2022-01-31'
ORDER BY missing_date;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/a375801a-6650-4878-8104-85c59e82fe8d)

Task-04
```sql
CREATE VIEW v_symmetric_union AS (
	SELECT person_id FROM (
		SELECT * FROM person_visits pv1
		WHERE visit_date = '2022-01-02'
		EXCEPT
		SELECT * FROM person_visits pv2
		WHERE visit_date = '2022-01-06'
	) as except1
	UNION
	SELECT person_id FROM (
		SELECT * FROM person_visits pv2
		WHERE visit_date = '2022-01-06'
		EXCEPT
		SELECT * FROM person_visits pv1
		WHERE visit_date = '2022-01-02'
	) as except2
ORDER BY person_id
);
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/75e5dbc0-06d4-489d-9324-5e067d6cb4fb)
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/f3691b94-6d68-4561-9207-10659c3a269e)

Task-05
```sql
CREATE VIEW v_price_with_discount AS (
	SELECT p.name, m.pizza_name, m.price, ROUND(m.price - m.price * 0.1) AS discount_price
	FROM person_order po
	JOIN person p ON p.id = po.person_id
	JOIN menu m ON m.id = po.menu_id
  ORDER BY name, pizza_name
);
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/a7dcc9a0-9fcc-43b4-95a7-68ef86fc53ad)

Task-06
```sql
CREATE MATERIALIZED VIEW mv_dmitriy_visits_and_eats AS (
	SELECT pz.name FROM person_visits pv
	JOIN person p ON pv.person_id = p.id
	JOIN pizzeria pz ON pv.pizzeria_id = pz.id
	WHERE pv.visit_date = '2022-01-08' and p.name = 'Dmitriy'
);
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/1ef68ea7-be9f-4efa-ad5f-53e42141b43b)

Task-07
```sql
INSERT INTO person_visits 
VALUES (
	(SELECT MAX(id)+1 FROM person_visits),
	(SELECT id FROM person WHERE name = 'Dmitriy'),
	(SELECT pizzeria_id FROM menu WHERE price < 800 AND menu.pizzeria_id = (SELECT pz.id FROM pizzeria pz WHERE name = 'DoDo Pizza')),
	'2022-01-08'
);

REFRESH MATERIALIZED VIEW mv_dmitriy_visits_and_eats;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/8b086a76-8076-4bd0-8980-fa49b53d7a5a)

Task-08
```sql
DROP VIEW v_generated_dates;
DROP VIEW v_persons_female;
DROP VIEW v_persons_male;
DROP VIEW v_price_with_discount;
DROP VIEW v_symmetric_union;
DROP MATERIALIZED VIEW mv_dmitriy_visits_and_eats;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/b73b7400-5e7c-4d8c-8b06-172b55c52697)

