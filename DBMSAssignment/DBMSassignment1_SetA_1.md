# Assignment 1 – Set A – Q1: Player Table

## Lab-book task
Create Player(player_id, Name, Birth_date, Birth_place) with player_id primary key and a table-level NOT NULL constraint on Name.

## Solution
```sql
DROP TABLE IF EXISTS Player CASCADE;
CREATE TABLE Player (
    player_id   INTEGER PRIMARY KEY,
    name        VARCHAR(50),
    birth_date  DATE,
    birth_place VARCHAR(100),
    CONSTRAINT player_name_not_null CHECK (name IS NOT NULL)
);

-- Test
INSERT INTO Player VALUES
(1, 'Sachin', DATE '1973-04-24', 'Mumbai');
SELECT * FROM Player;
```

## Notes / assumptions
PostgreSQL supports a table-level CHECK constraint to enforce the workbook’s table-level “Name should not be NULL” requirement.
