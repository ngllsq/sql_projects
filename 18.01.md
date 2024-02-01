## Task- 5
```sql
SELECT
	p.id AS "person.id",
	p.name AS "person.name",
	age,
	gender,
	address,
	pi.id AS "pizzeria.id",
	pi.name AS "pizzeria.name",
	rating
FROM person p
CROSS JOIN pizzeria pi 
ORDER BY "person.id", "pizzeria.id";
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/320df894-84da-4942-aa7c-321615851f75)

## Task- 6
```sql
SELECT 
	po.order_date AS action_date,
	p.name
FROM person_order po
JOIN person_visits pv ON po.order_date = pv.visit_date AND po.person_id = pv.person_id
JOIN person p ON po.person_id = p.id
ORDER BY action_date ASC, name DESC;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/f0e3c75c-cce7-4163-8acf-9c7bb82116e4)

## Task - 7
```sql
SELECT 
	po.order_date,
	p.name || '(age: ' || p.age ||')' AS person_information
FROM person_order po
JOIN person p ON po.person_id = p.id;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/b1c5fed7-5e5b-4d55-9770-c4b07b4ab3f5)

## Task - 8
```sql
SELECT order_date, name || '(age: ' || age || ')'   AS person_information
FROM (SELECT order_date, person_id AS id FROM person_order) as tab
NATURAL JOIN  person;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/c4821eab-2920-4488-8cc5-b83ee369acca)

## Task - 9
```sql
SELECT name FROM pizzeria WHERE id NOT IN (SELECT pizzeria_id FROM person_visits);
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/06ed5d0d-e3da-403f-9cd6-0a9d56aaf85e)

```sql
SELECT name 
FROM pizzeria
WHERE NOT EXISTS(SELECT pizzeria_id FROM person_visits WHERE pizzeria.id = pizzeria_id);
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/ee3f57c5-b0c4-4f33-87b3-9476b907cc27)

## Task - 10
```sql
SELECT 
	p.name AS person_name,
	m.pizza_name AS pizza_name,
	pi.name AS pizzeria_name
FROM person p
JOIN person_order ON person_id = p.id
JOIN menu m ON m.id = person_order.menu_id
JOIN pizzeria pi ON m.pizzeria_id = pi.id
ORDER BY person_name, pizza_name, pizzeria_name 
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/00e8f701-9eb8-477e-bac6-fe9b51bb2efa)

