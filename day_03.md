## Task 00
```sql
SELECT
	m.pizza_name,
	m.price,
	pi.name AS pizzeria_name,
	pv.visit_date
FROM person_visits pv
JOIN person p ON pv.person_id = p.id
JOIN menu m ON pv.pizzeria_id = m.pizzeria_id
JOIN pizzeria pi ON pi.id = pv.pizzeria_id
WHERE (p.name = 'Kate') AND (m.price BETWEEN 800 AND 1000)
ORDER BY 1, 2, 3;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/46995252-6c8d-4dc1-9d2a-f80365fd35cc)

## Task 01
```sql
SELECT 
	m.id
FROM menu m
LEFT JOIN person_order po ON po.menu_id = m.id
WHERE po.menu_id IS NULL
ORDER BY 1;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/279e20cb-2685-4aab-9dd0-76861c2005db)


## Task 02
```sql
SELECT 
	m.pizza_name,
	m.price,
	pi.name AS pizzeria_name
FROM menu m
LEFT JOIN person_order po ON po.menu_id = m.id
JOIN pizzeria pi ON m.pizzeria_id = pi.id
WHERE po.menu_id IS NULL
ORDER BY 1, 2;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/2b2031e9-cf3c-4c42-ab32-397d931882ec)


## Task 03
```sql

```

## Task 04
```sql

```

## Task 05
```sql

```

## Task 06
```sql

```

## Task 07
```sql

```

## Task 08
```sql

```

## Task 09
```sql

```

## Task 10
```sql

```

## Task 11
```sql

```

## Task 12
```sql

```

## Task 13
```sql

```

## Task 14
```sql

```
