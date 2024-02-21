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
SELECT days::date 
FROM generate_series('2022-01-01', '2022-01-10', interval '1 day') AS days
LEFT JOIN person_visits pv ON days = pv.visit_date AND (pv.person_id = 1 OR pv.person_id = 2)
WHERE pv.visit_date IS NULL
ORDER BY 1 ASC;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/08134e2a-867b-4762-a3da-864933a06edb)

## Task 02
```sql
SELECT
 COALESCE(p.name, '-') AS person_name,
 tab.visit_date,
 COALESCE(pi.name, '-') AS pizzeria_name
 FROM person p
 FULL JOIN (
 SELECT pizzeria_id, person_id, visit_date FROM person_visits
 WHERE visit_date BETWEEN '2022-01-01' AND '2022-01-03'
) tab ON tab.person_id = p.id
FULL JOIN pizzeria pi ON pi.id = tab.pizzeria_id
ORDER BY 1, 2, 3
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/4398e3a2-484f-4a7b-a29a-44438e4c3737)



## Task 03
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

## Task 04
```sql
SELECT m.pizza_name, pi.name, m.price FROM menu m 
JOIN pizzeria pi ON pi.id = m.pizzeria_id
WHERE m.pizza_name = 'pepperoni pizza' OR m.pizza_name = 'mushroom pizza'
ORDER BY 1, 2;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/60b2bfbd-df95-4353-855c-de598e4285e9)



## Task 05
```sql
SELECT p.name FROM person p
WHERE p.age > 25 AND p.gender = 'female'
ORDER BY 1;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/07306ae2-e69d-4577-9125-9c23737f954a)


## Task 06
```sql
SELECT 
	m.pizza_name,
	pi.name AS pizzeria_name
FROM menu m
JOIN pizzeria pi ON m.pizzeria_id = pi.id
JOIN person_order po ON m.id = po.menu_id 
JOIN person p ON po.person_id = p.id
WHERE p.name = 'Denis' OR p.name = 'Anna'
ORDER BY 1, 2;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/06e7e04a-065a-4f2d-811c-60c57fb77029)

## Task 07
```sql
SELECT pi.name,
FROM pizzeria pi
JOIN person_visits pv ON pv.pizzeria_id = pi.id
JOIN person p ON p.id= pv.person_id
JOIN menu m ON pi.id = m.pizzeria_id
WHERE p.name = 'Dmitriy' AND m.price < 800 AND pv.visit_date = '2022.01.08';
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/8882b5f9-82e0-4546-b359-46a8311865fa)

## Task 08
```sql
SELECT p.name FROM person p
JOIN person_order po ON po.person_id = p.id
JOIN menu m ON m.id = po.menu_id
WHERE (p.gender = 'male') 
AND (p.address = 'Moscow' OR p.address = 'Samara') 
AND (m.pizza_name = 'pepperoni pizza' OR m.pizza_name = 'mushroom pizza')
ORDER BY 1 DESC;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/49d92bb2-494f-4e02-aede-322a95d67eaa)



## Task 09
```sql
SELECT DISTINCT p.name
FROM person p
JOIN person_order po ON p.id = po.person_id
JOIN menu m ON po.menu_id = m.id 
WHERE (p.gender = 'female') AND  (m.pizza_name = 'cheese pizza' OR  m.pizza_name = 'pepperoni pizza')
ORDER BY 1;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/caf75c49-b345-4213-b962-28ae0b32f785)


## Task 10
```sql
SELECT 
	p1.name AS person_name1, 
	p2.name AS person_name2, 
	p1.address AS common_address 
FROM person p1
JOIN person AS p2 ON (p1.address = p2.address) AND (p1.name > p2.name)
ORDER BY 1, 2, 3;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/58ffb2cf-5f02-4b78-838f-785176268e7e)
