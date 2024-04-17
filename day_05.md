## Task 00
```sql
CREATE INDEX idx_menu_pizzeria_id ON menu(pizzeria_id);
CREATE INDEX idx_person_visits_person_id ON person_visits(person_id);
CREATE INDEX idx_person_visits_pizzeria_id ON person_visits(pizzeria_id);
CREATE INDEX idx_person_order_person_id ON person_order(person_id);
CREATE INDEX idx_person_order_menu_id ON person_order(menu_id);
```

## Task 01
```sql
EXPLAIN ANALYZE
SELECT m.pizza_name, p.name AS pizzeria_name
FROM menu m
JOIN pizzeria p ON m.pizzeria_id = p.id;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/2618c02c-39d4-467b-a206-a2ba64764d3f)

## Task 02
```sql
```
