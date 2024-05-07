## Task 00
```sql
CREATE TABLE person_discounts (
    id INT PRIMARY KEY,
    person_id INT,
    pizzeria_id INT,
    discount DECIMAL(5,2),
    FOREIGN KEY (person_id) REFERENCES person(id),
    FOREIGN KEY (pizzeria_id) REFERENCES pizzeria(id),
    CONSTRAINT fk_person_discounts_person_id FOREIGN KEY (person_id) REFERENCES person(id),
    CONSTRAINT fk_person_discounts_pizzeria_id FOREIGN KEY (pizzeria_id) REFERENCES pizzeria(id)
);
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/5ed23e50-d726-4fa6-91f6-e1ab070f6ef2)


## Task 01
```sql
INSERT INTO person_discounts (id, person_id, pizzeria_id, discount)
SELECT 
    ROW_NUMBER() OVER () AS id,
    po.person_id,
    pi.id,
    CASE 
        WHEN COUNT(po.person_id) = 1 THEN 10.5 
        WHEN COUNT(po.person_id) = 2 THEN 22 
        ELSE 30 
    END AS discount
FROM person_order po
JOIN menu m ON po.menu_id = m.id
JOIN pizzeria pi ON pi.id = m.pizzeria_id
GROUP BY po.person_id, pi.id;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/82b2fef6-974c-47d0-bc78-536e6cae1a02)


## Task 02
```sql
SELECT
  p.name AS person_name,
  m.pizza_name,
  m.price AS original_price,
  ROUND(m.price - (m.price * pd.discount / 100)) AS discounted_price,
  piz.name AS pizzeria_name
FROM menu m
JOIN person_order po ON po.menu_id = m.id
JOIN person p ON p.id = po.person_id
JOIN person_discounts pd ON pd.person_id = p.id AND pd.pizzeria_id = m.pizzeria_id
JOIN pizzeria piz ON piz.id = m.pizzeria_id
ORDER BY person_name, pizza_name, discounted_price DESC, pizzeria_name;
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/88beea86-da1d-4d46-bada-f50af7ddfea2)

## Task 03
```sql
CREATE UNIQUE INDEX idx_person_discounts_unique ON person_discounts(person_id, pizzeria_id);
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/37b33b26-61c5-4a42-950c-0e122f88839c)


## Task 04
```sql
ALTER TABLE person_discounts
ADD CONSTRAINT ch_nn_person_id CHECK (person_id IS NOT NULL);

ALTER TABLE person_discounts
ADD CONSTRAINT ch_nn_pizzeria_id CHECK (pizzeria_id IS NOT NULL);

ALTER TABLE person_discounts
ADD CONSTRAINT ch_nn_discount CHECK (discount IS NOT NULL);

ALTER TABLE person_discounts
ALTER COLUMN discount SET DEFAULT 0;

ALTER TABLE person_discounts
ADD CONSTRAINT ch_range_discount CHECK (discount >= 0 AND discount <= 100);
```

## Task 05
```sql
COMMENT ON TABLE person_discounts IS 'Эта таблица хранит информацию о скидках для каждого человека в различных пиццериях.';
COMMENT ON COLUMN person_discounts.person_id IS 'Идентификатор человека';
COMMENT ON COLUMN person_discounts.pizzeria_id IS 'Идентификатор пиццерии';
COMMENT ON COLUMN person_discounts.discount IS 'Процент скидки для человека в пиццерии';
```

## Task 06
```sql
DO $$
BEGIN
    IF (SELECT COUNT(*) FROM person_discounts) = 0 THEN
        EXECUTE 'CREATE SEQUENCE seq_person_discounts START 1';
    ELSE
        EXECUTE 'CREATE SEQUENCE seq_person_discounts START ' || ((SELECT COUNT(*) FROM person_discounts) + 1);
    END IF;
END $$;

ALTER TABLE person_discounts ALTER COLUMN id SET DEFAULT nextval('seq_person_discounts');
```
![image](https://github.com/ngllsq/sql_projects/assets/114596475/41d9cd0e-fe51-4749-a7e0-f2cf269d54db)
