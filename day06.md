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

```

Task-03
```sql

```

Task-04
```sql

```

Task-05
```sql

```

Task-06
```sql

```
