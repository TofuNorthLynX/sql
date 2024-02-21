Task-00
```sql
SELECT pv.person_id, COUNT(pv.id) as count_of_visits 
FROM person_visits pv
GROUP BY 1
ORDER BY 2 DESC, 1;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/bbe83df7-c808-479a-95a1-5eacad1817e8)

Task-01
```sql
SELECT p.name, COUNT(pv.id) as count_of_visits 
FROM person_visits pv
JOIN person p ON p.id = pv.person_id
GROUP BY 1
ORDER BY 2 DESC, 1 LIMIT 4;
```
![image](https://github.com/TofuNorthLynX/sql/assets/112647131/8be209fe-9875-4699-a9a0-c17d19fe2703)

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

Task-07
```sql

```

Task-08
```sql

```

Task-09
```sql

```
