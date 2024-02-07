## Task 1
```sql
SELECT id AS object_id, pizza_name AS object_name FROM menu
UNION ALL
SELECT id, name FROM person
ORDER BY 1,2;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/84c60a83-6817-4fb2-b297-1c935e799627)

## Task 2
```sql
SELECT object_name FROM (
	SELECT pizza_name AS object_name, 'pizza' AS type FROM menu
	UNION ALL
	SELECT name, 'name' FROM person
	ORDER BY TYPE ASC
) AS tablee;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/f17c716b-6746-4e7d-ada4-0a4dd79328f0)


## Task 3
```sql
SELECT po.order_date, po.person_id
FROM person_order po
JOIN person_visits pv ON po.person_id = pv.person_id AND po.order_date = pv.visit_date
ORDER BY po.order_date, po.person_id DESC;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/1269d4a8-339c-42d5-8fe4-a07c1891c586)

## Task 4
```sql
SELECT person_id FROM person_order WHERE order_date = '2022-01-07'
EXCEPT ALL
SELECT person_id FROM person_visits WHERE visit_date = '2022-01-07';
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/3154b93f-3286-42b8-a797-c3dfcf4c849a)

## Task 5
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

## Task 6
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

## Task 7
```sql
SELECT 
	po.order_date,
	p.name || '(age: ' || p.age ||')' AS person_information
FROM person_order po
JOIN person p ON po.person_id = p.id
ORDER BY 1,2;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/f89aa4cd-9b44-4a5a-9c5c-512e9de345c7)


## Task 8
```sql
SELECT order_date, name || '(age: ' || age || ')'   AS person_information
FROM (SELECT order_date, person_id AS id FROM person_order) as tab
NATURAL JOIN  person
ORDER BY 1,2;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/95203442-e653-4539-992e-d4629197a28e)

## Task 9
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

## Task 10
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

