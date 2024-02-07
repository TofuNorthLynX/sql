Task-01
```sql

```

Task-01
```sql

```

Task-02
```sql

```

Task-03
```sql

```

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

```

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
