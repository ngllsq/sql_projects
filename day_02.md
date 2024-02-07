## Task 00
```sql
SELECT
	pi.name,
	pi.rating
FROM pizzeria pi
LEFT JOIN person_visits pv ON pi.id = pizzeria_id 
WHERE pv.id IS NULL
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/6e4f28c6-6fca-4b83-8d4b-b64c077f26b8)

## Task 01
```sql
WITH all_days AS (
  SELECT days::date 
  FROM generate_series('2022-01-01', '2022-01-10', interval '1 day') AS days
)
SELECT all_days.days 
FROM all_days
LEFT JOIN person_visits pv ON all_days.days = pv.visit_date AND (pv.person_id = 1 OR pv.person_id = 2)
WHERE pv.visit_date IS NULL
ORDER BY 1 ASC;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/08134e2a-867b-4762-a3da-864933a06edb)

## Task 09
```sql
SELECT DISTINCT p.name
FROM person p
JOIN person_order po ON p.id = po.person_id
JOIN menu m ON po.menu_id = m.id AND m.pizza_name = 'pepperoni pizza'
WHERE p.gender = 'female' 
AND EXISTS (
    SELECT 
    FROM person_order po
    JOIN menu m ON po.menu_id = m.id AND m.pizza_name = 'cheese pizza'
    WHERE po.person_id = p.id
)
ORDER BY p.name;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/6520b13d-6ba0-45de-a10f-53caea625676)

