# Assignment 1 – Set B – Q1: Machine Table

## Lab-book task
Create Machine with uppercase non-null name, restricted machine type, positive price, and machine_cost < machine_price.

## Solution
```sql
DROP TABLE IF EXISTS Machine CASCADE;
CREATE TABLE Machine (
    machine_id    INTEGER PRIMARY KEY,
    machine_name  VARCHAR(50) NOT NULL,
    machine_type  VARCHAR(10),
    machine_price  DOUBLE PRECISION,
    machine_cost   DOUBLE PRECISION,
    CONSTRAINT machine_name_upper CHECK (machine_name = UPPER(machine_name)),
    CONSTRAINT machine_type_chk CHECK (machine_type IN ('drilling','milling','lathe','turning','grinding')),
    CONSTRAINT machine_price_chk CHECK (machine_price > 0),
    CONSTRAINT machine_cost_chk CHECK (machine_cost < machine_price)
);
```
