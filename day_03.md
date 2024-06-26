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
WITH orders_woman AS (
	SELECT pi.name FROM person_order po
	JOIN menu m ON m.id = po.menu_id
	JOIN pizzeria pi ON pi.id = m.pizzeria_id
	JOIN person p ON p.id = po.person_id
	WHERE p.gender = 'female'
), orders_men as (
	SELECT pi.name FROM person_order po
	JOIN menu m ON m.id = po.menu_id
	JOIN pizzeria pi ON pi.id = m.pizzeria_id
	JOIN person p ON p.id = po.person_id
	WHERE p.gender = 'male'
)

(
	SELECT * FROM orders_woman
	EXCEPT ALL
	SELECT * FROM orders_men
)
UNION 
(
	SELECT * FROM orders_men
	EXCEPT ALL
	SELECT * FROM orders_woman
)
ORDER BY 1;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/8bc943d9-4762-4a6c-adf8-bf84bbb104b8)


## Task 04
```sql
WITH orders_woman AS (
	SELECT pi.name AS pizzeria_name FROM person_order po
	JOIN menu m ON m.id = po.menu_id
	JOIN pizzeria pi ON pi.id = m.pizzeria_id
	JOIN person p ON p.id = po.person_id
	WHERE p.gender = 'female'
), orders_men as (
	SELECT pi.name FROM person_order po
	JOIN menu m ON m.id = po.menu_id
	JOIN pizzeria pi ON pi.id = m.pizzeria_id
	JOIN person p ON p.id = po.person_id
	WHERE p.gender = 'male'
)

(
	SELECT * FROM orders_woman
	EXCEPT
	SELECT * FROM orders_men
)
UNION
(
	SELECT * FROM orders_men
	EXCEPT
	SELECT * FROM orders_woman
);
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/dda3d8ef-a58a-4cdf-90d3-021283d3aeec)



## Task 05
```sql
SELECT
	pi.name AS pizzeria_name
FROM pizzeria pi
JOIN person_visits pv ON pi.id = pv.pizzeria_id 
JOIN person p ON p.id = pv.person_id
WHERE p.name = 'Andrey'

EXCEPT

SELECT DISTINCT
	pi.name AS pizzeria_name
FROM pizzeria pi
JOIN menu m ON m.pizzeria_id = pi.id
JOIN person_order po ON po.menu_id = m.id
JOIN person p ON p.id = po.person_id
WHERE p.name = 'Andrey'
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/2912d06f-ad72-458c-8d54-df999c2a9899)

## Task 06
```sql
SELECT m1.pizza_name, p1.name AS pizzeria_name_1, p2.name AS pizzeria_name_2, m1.price
FROM menu m1
JOIN menu m2 ON m1.pizza_name = m2.pizza_name AND m1.price = m2.price AND m1.pizzeria_id <> m2.pizzeria_id
JOIN pizzeria p1 ON m1.pizzeria_id = p1.id
JOIN pizzeria p2 ON m2.pizzeria_id = p2.id
WHERE p1.id > p2.id
ORDER BY 1;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/fed7c698-de77-4b8d-bcfc-0c8b96e27f72)


## Task 07
```sql
INSERT INTO menu
VALUES (19, 2, 'greek pizza', 800);
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/c71659d5-77b0-4ff0-8f3f-b8c1e81e418f)

```sql
UPDATE pizzeria
SET name = 'Dominos'
WHERE id = 2;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/3253ae64-a38e-49e1-837e-efde91abb9fa)


## Task 08
```sql
INSERT INTO menu
VALUES(
	(SELECT MAX(id) + 1 FROM menu),
	(SELECT id FROM pizzeria WHERE name = 'Dominos'),
	'sicilian pizza',
	900);
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/641e7ba2-87e3-4f10-bd51-3250e8a6a1c9)


## Task 09
```sql
INSERT INTO person_visits
VALUES(
	(SELECT MAX(id) + 1 FROM person_visits),
	(SELECT id FROM person WHERE name = 'Denis'),
	(SELECT id FROM pizzeria WHERE name = 'Dominos'),
	'2022-02-24'),
(
	(SELECT MAX(id) + 2 FROM person_visits),
	(SELECT id FROM person WHERE name = 'Irina'),
	(SELECT id FROM pizzeria WHERE name = 'Dominos'),
	'2022-02-24');
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/efe1adfd-8423-4398-bd65-97ce5bd653d2)

## Task 10
```sql
INSERT INTO person_order
VALUES(
	(SELECT MAX(id) + 1 FROM person_visits),
	(SELECT id FROM person WHERE name = 'Denis'),
	(SELECT id FROM menu WHERE pizza_name = 'sicilian pizza'),
	'2022-02-24'),
(
	(SELECT MAX(id) + 2 FROM person_visits),
	(SELECT id FROM person WHERE name = 'Irina'),
	(SELECT id FROM menu WHERE pizza_name = 'sicilian pizza'),
	'2022-02-24');
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/a7bfe6f5-623b-44a8-a51c-a39325c64317)

## Task 11
```sql
UPDATE menu
SET price = price * 0.9
WHERE pizza_name = 'greek pizza';
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/ff97df9b-389c-4990-83b7-386259e5479a)


## Task 12
```sql
INSERT INTO person_order (id, person_id, menu_id, order_date)
SELECT (SELECT COALESCE(MAX(id), 0) FROM person_order) + id, id, (SELECT id FROM menu WHERE pizza_name = 'greek pizza'), '2022-02-25'
FROM person;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/afa19769-87b5-4cc9-9415-03a85d30cbd7)

## Task 13
```sql
DELETE FROM person_order
WHERE order_date = '2022-02-25';
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/504ce717-53ab-4c6a-b5b3-10967c26e0e2)

```sql
DELETE FROM menu
WHERE pizza_name = 'greek pizza';
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/b024c406-8ec4-4a4c-abce-ba2dd1e9b145)



