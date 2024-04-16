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
```
