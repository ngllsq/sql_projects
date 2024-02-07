# Task - 1
```sql
SELECT name, person.age, person.address FROM person
WHERE address = 'Kazan';
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/8a5bc442-4970-433c-93ce-e75f21592ed3)

# Task - 2
```sql
SELECT name, person.gender, person.age, person.address FROM person
WHERE address = 'Kazan' AND gender = 'female'
ORDER BY name; 
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/1a09dc62-6eee-468c-8d13-18ce92254070)

# Task - 3
```sql
SELECT name, rating FROM pizzeria
WHERE rating BETWEEN 3.5 AND 5;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/ccf41861-d181-4bad-8f8e-5c981c571b56)
```sql
SELECT name, rating FROM pizzeria
WHERE rating >= 3.5 AND rating <= 5;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/435e1b07-c471-4ed0-b23f-b7d2644f275c)

# Task - 4
```sql
SELECT DISTINCT person_id FROM person_visits
WHERE pizzeria_id = 2 OR visit_date BETWEEN '2022-01-01' AND '2022-01-04'
ORDER BY person_id DESC;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/fcc7698a-46ed-49c9-b610-f5e4f8b1ca13)

# Task - 5
```sql
SELECT name FROM person WHERE id IN(
SELECT id
FROM person_order
WHERE menu_id = 1);
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/aa792b73-f1eb-47fd-b354-dcf267ef0e5c)

# Task - 6
```sql
SELECT EXISTS (SELECT FROM person WHERE name = 'Anna');
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/91c42618-da73-4780-b92f-fcf1cd803da6)

#Task - 7
```sql
SELECT id AS object_id, pizza_name AS object_name FROM menu
UNION
SELECT id, name FROM person
ORDER BY 1,2;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/84c60a83-6817-4fb2-b297-1c935e799627)

#Task - 8
```sql
SELECT object_name FROM (
	SELECT pizza_name AS object_name, 'pizza' AS type FROM menu
	UNION ALL
	SELECT name, 'name' FROM person
	ORDER BY TYPE DESC
) AS tablee;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/d83b8197-3321-4e88-94ae-f5d0328e532d)

#Task - 9
```sql
SELECT po.order_date, po.person_id
FROM person_order po
JOIN person_visits pv ON po.person_id = pv.person_id AND po.order_date = pv.visit_date
ORDER BY po.order_date, po.person_id DESC;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/1269d4a8-339c-42d5-8fe4-a07c1891c586)

#Task - 10
```sql
SELECT person_id FROM person_order WHERE order_date = '2022-01-07'
EXCEPT ALL
SELECT person_id FROM person_visits WHERE visit_date = '2022-01-07';
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/3154b93f-3286-42b8-a797-c3dfcf4c849a)
