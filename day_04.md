## Task 00
```sql
CREATE VIEW v_persons_female AS
SELECT * FROM person
WHERE gender = 'female';
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/1a4e33b1-952c-4afb-9542-b4ae2b2f9fdb)

```sql
CREATE VIEW v_persons_male AS
SELECT * FROM person
WHERE gender = 'male';
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/32a0577d-13ca-4397-b234-65283a17c437)

## Task 01
```sql
SELECT name FROM v_persons_female
UNION
SELECT name FROM v_persons_male
ORDER BY 1;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/75deb8aa-6adc-4eea-861d-77b850d08b7c)


## Task 02
```sql
CREATE VIEW v_generated_dates AS
SELECT generate_series::date AS generated_date
FROM generate_series('2022-01-01', '2022-01-31', interval '1 day')
ORDER BY generated_date;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/30e51c7f-06a9-4a45-b647-3e087dcffa3e)

## Task 03
```sql
SELECT generated_date AS missing_date FROM v_generated_dates
WHERE generated_date NOT IN (SELECT visit_date FROM person_visits)
ORDER BY missing_date;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/49c91d38-c178-488a-9ae4-9d21d92482eb)

## Task 04
```sql
CREATE VIEW v_symmetric_union AS
SELECT person_id
FROM person_visits
WHERE visit_date BETWEEN '2022-01-01' AND '2022-01-02'
EXCEPT
SELECT person_id
FROM person_visits
WHERE visit_date BETWEEN '2022-01-01' AND '2022-01-06'
UNION
SELECT person_id
FROM person_visits
WHERE visit_date BETWEEN '2022-01-01' AND '2022-01-06'
EXCEPT
SELECT person_id
FROM person_visits
WHERE visit_date BETWEEN '2022-01-01' AND '2022-01-02'
ORDER BY 1;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/3a7c90c4-1280-47ec-b455-e4ee4478f727)

## Task 05
```sql
CREATE VIEW v_price_with_discount AS
SELECT p.name, 
	m.pizza_name, 
	m.price,
	ROUND(m.price - m.price * 0.1) AS discount_price
FROM person p
JOIN person_order po ON p.id = po.person_id
JOIN menu m ON po.menu_id = m.id
ORDER BY 1;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/75a85af6-fc53-40f7-ba4f-ffa9c389e946)

## Task 06
```sql
CREATE MATERIALIZED VIEW  mv_dmitriy_visits_and_eats AS
SELECT pi.name FROM pizzeria pi
JOIN person_visits pv ON pv.pizzeria_id = pi.id
JOIN menu m ON m.pizzeria_id = pv.pizzeria_id
JOIN person p ON pv.person_id = p.id
WHERE m.price < 800 AND pv.visit_date = '2022-01-08' AND p.name = 'Dmitriy';
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/aa5a85b2-6349-4df2-9d9a-f1e3c6581d92)

## Task 07
```sql
INSERT INTO person_visits 
VALUES ((SELECT MAX(id) + 1 FROM person_visits),
	   (SELECT id FROM person WHERE name = 'Dmitriy'),
	   (SELECT pizzeria_id FROM menu WHERE price < 800 AND pizzeria_id NOT IN (SELECT id FROM pizzeria WHERE name = 'Papa Johns') LIMIT 1),
	   '2022-01-08');
```
```sql
REFRESH MATERIALIZED VIEW mv_dmitriy_visits_and_eats;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/3629cc3d-6b12-4b20-a0d6-cda55e81786c)

## Task 08
```sql
DROP VIEW IF EXISTS v_persons_female;
DROP VIEW IF EXISTS v_persons_male;
DROP VIEW IF EXISTS v_generated_dates;
DROP VIEW IF EXISTS v_symmetric_union;
DROP VIEW IF EXISTS v_price_with_discount;
DROP MATERIALIZED VIEW IF EXISTS mv_dmitriy_visits_and_eats;
```
