# Assignment 1 – Set B – Q2: Employee Table

## Lab-book task
Create Employee with uppercase non-null name, restricted designation, positive salary, unique UID, and employee_uid <> employee_id.

## Solution
```sql
DROP TABLE IF EXISTS Employee CASCADE;
CREATE TABLE Employee (
    employee_id   INTEGER PRIMARY KEY,
    employee_name VARCHAR(50) NOT NULL,
    employee_desg VARCHAR(10),
    employee_sal  DOUBLE PRECISION,
    employee_uid  TEXT UNIQUE,
    CONSTRAINT employee_name_upper CHECK (employee_name = UPPER(employee_name)),
    CONSTRAINT employee_desg_chk CHECK (employee_desg IN ('Manager','staff','worker')),
    CONSTRAINT employee_sal_chk CHECK (employee_sal > 0),
    CONSTRAINT employee_uid_diff CHECK (employee_uid <> employee_id::TEXT)
);
```
