# sql

Task-2

```sql
  SELECT name, age FROM person
  WHERE address = 'Kazan';
```  
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/0c892d74-ea12-49cd-a487-5e7058d506a4)

Task-3
```sql
SELECT name, age FROM person
WHERE address = 'Kazan' and gender = 'female'
ORDER BY name;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/13eb330f-b8cd-4618-8f20-61618056f973)

Task-4
```sql
SELECT name, rating 
FROM pizzeria pi
WHERE pi.rating >= 3.5 and pi.rating <= 5
ORDER BY rating;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/e26d3984-d6a1-44e3-bd04-22ad97b9bdf9)

Task-5
```sql
SELECT DISTINCT person_id 
FROM person_visits
WHERE visit_date BETWEEN '2022-01-03' AND '2022-01-07' or pizzeria_id = 2
ORDER BY person_id DESC;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/95905eed-1121-4b45-929c-e6f9fcbddd6f)

Task-6
```sql
SELECT name
FROM person 
WHERE id IN(
  SELECT person_id 
  FROM person_order 
	WHERE order_date = '2022-01-03' or order_date = '2022-01-05' or order_date = '2022-01-07'
);
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/813e916a-e64a-4e02-ae05-0e3c081076f0)

Task-7
```sql
SELECT EXISTS(
	SELECT name FROM person WHERE name = 'Irina'
);
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/b19a8b30-0e9a-4464-b25f-d16a8f1aeab8)
