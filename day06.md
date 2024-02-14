Task-00
```sql
CREATE TABLE person_discounts (
	id BIGINT PRIMARY KEY,
	person_id BIGINT NOT NULL,
	pizzeria_id BIGINT NOT NULL,
	discount FLOAT DEFAULT NULL,
	CONSTRAINT fk_person_discounts_person_id FOREIGN KEY (person_id) REFERENCES person(id),
	CONSTRAINT fk_person_discounts_pizzeria_id FOREIGN KEY (pizzeria_id) REFERENCES pizzeria(id)
);
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/2529c87a-e5bf-4751-b2f8-31e750d8cddb)

Task-01
```sql
WITH amount_of_orders AS (
	SELECT po.person_id, m.pizzeria_id, COUNT(*) FROM person_order po
	JOIN menu m ON m.id = po.menu_id
	GROUP BY 1, 2 
	ORDER BY 1, 2 
)

INSERT INTO person_discounts
	SELECT
	ROW_NUMBER() OVER(ORDER BY 1) AS id,
	person_id,
	pizzeria_id,
	CASE
		WHEN count = 1 THEN 10.5
		WHEN count = 2 THEN 22
		ELSE 30
	END
	FROM amount_of_orders
;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/86f99255-5a28-49d1-8fb1-9d5fb2eb3f1e)

Task-02
```sql
SELECT p.name, 
	m.pizza_name, 
	m.price, 
	(m2.price - ((m2.price * pd.discount) / 100)) as discount_price,
	piz.name as pizzeria_name
	FROM menu m

JOIN person_order po ON po.menu_id = m.id
JOIN person p ON p.id = po.person_id
JOIN person_discounts pd ON pd.person_id = po.person_id
JOIN menu m2 ON m.id = m2.id
JOIN pizzeria piz ON piz.id = m.pizzeria_id
ORDER BY 1, 2, 4 DESC, 5;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/e3701d31-0e78-4b54-8428-939bcd672818)

Task-04
```sql
ALTER TABLE person_discounts 
	ADD CONSTRAINT ch_nn_person_id CHECK (person_id IS NOT NULL);
ALTER TABLE person_discounts 
	ADD CONSTRAINT ch_nn_pizzeria_id CHECK (pizzeria_id IS NOT NULL);
ALTER TABLE person_discounts 
	ADD CONSTRAINT ch_nn_discount CHECK (discount IS NOT NULL);
ALTER TABLE person_discounts 
	ALTER discount SET DEFAULT 0;
ALTER TABLE person_discounts 
	ADD CONSTRAINT ch_range_discount CHECK (discount BETWEEN 0 AND 100);
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/5c45908c-c672-4320-a4b5-c27ed06b6717)

Task-05
```sql

```

Task-06
```sql

```
