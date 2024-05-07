## Task 00
```sql
SELECT person_id, COUNT(*) AS count_of_visits
FROM person_visits
GROUP BY person_id
ORDER BY count_of_visits DESC, person_id ASC;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/e9cbe376-9445-443d-b930-ab0319d41a6a)

## Task 01
```sql
SELECT p.name, COUNT(*) AS count_of_visits
FROM person p
JOIN person_visits v ON p.id = v.person_id
GROUP BY p.name
ORDER BY 1
LIMIT 4;
```

## Task 02
```sql
(
  SELECT pi.name, COUNT(*) AS count, 'order' AS action_type
  FROM person_order po
  JOIN menu m ON m.id = po.menu_id
  JOIN pizzeria pi ON m.pizzeria_id = pi.id
  GROUP BY pi.name

  UNION ALL

  SELECT pi.name, COUNT(*) AS count, 'visit' AS action_type
  FROM person_visits pv
  JOIN pizzeria pi ON pv.pizzeria_id = pi.id
  GROUP BY pi.name
)
ORDER BY action_type ASC, count DESC;
```

## Task 03
```sql
WITH 
    orders_data AS (
        SELECT pi.name, COUNT(*) AS count, 'order' AS action_type
        FROM person_order po
        JOIN menu m ON m.id = po.menu_id
        JOIN pizzeria pi ON m.pizzeria_id = pi.id
        GROUP BY pi.name
    ),
    visits_data AS (
        SELECT pi.name, COUNT(*) AS count, 'visit' AS action_type
        FROM person_visits v
        JOIN pizzeria pi ON v.pizzeria_id = pi.id
        GROUP BY pi.name
    )

SELECT o.name, COALESCE(o.count, 0) + COALESCE(v.count, 0) AS total_count
FROM orders_data o
FULL JOIN visits_data v ON o.name = v.name
ORDER BY total_count DESC, o.name ASC;
```

## Task 04
```sql
SELECT p.name, COUNT(*) AS count_of_visits
FROM person p
JOIN person_visits v ON p.id = v.person_id
GROUP BY p.name
HAVING COUNT(*) > 3;
```

## Task 05
```sql
SELECT DISTINCT name
FROM person
WHERE id IN (SELECT DISTINCT person_id FROM person_order)
ORDER BY 1;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/695f1e99-8431-4a51-a06f-f302f2fe92ae)


## Task 06
```sql
SELECT 
    pi.name,
    COUNT(po.id) AS count_of_orders,
    ROUND(AVG(m.price), 2) AS average_price,
    MAX(m.price) AS max_price,
    MIN(m.price) AS min_price
FROM person_order po
JOIN menu m ON po.menu_id = m.id
JOIN pizzeria pi ON m.pizzeria_id = pi.id
GROUP BY pi.name
ORDER BY pi.name;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/084a8fdb-0508-4e24-ad31-fda26e6153a4)


## Task 07
```sql
SELECT ROUND(AVG(rating)::numeric, 4) AS global_rating
FROM pizzeria;
```

## Task 08
```sql
SELECT p.address, pi.name, COUNT(po.id) AS count_of_orders
FROM person_order po
JOIN menu m ON po.menu_id = m.id
JOIN pizzeria pi ON m.pizzeria_id = pi.id
JOIN person p ON po.person_id = p.id
GROUP BY p.address, pi.name
ORDER BY p.address, pi.name;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/77debc44-bb9e-4234-a5d6-447926de3c76)


## Task 09
```sql
SELECT 
    p.address,
    MAX(age) - (MIN(age) / MAX(age)) AS formula,
    AVG(age) AS average,
    (MAX(age) - (MIN(age) / MAX(age))) > AVG(age) AS comparison
FROM person p
GROUP BY p.address
ORDER BY p.address;
```
