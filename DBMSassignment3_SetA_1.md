# Assignment 3 – Set A – Q1: Supplier ALTER/DROP Exercise

## Lab-book task
Create Supplier and execute the requested ALTER/DROP sequence.

## Solution
```sql
DROP TABLE IF EXISTS Supplier CASCADE;
CREATE TABLE Supplier (
    supplier_no INTEGER,
    supplier_name VARCHAR(50),
    city CHAR(10),
    phone_no BIGINT,
    amount DOUBLE PRECISION
);

ALTER TABLE Supplier ADD CONSTRAINT supplier_pk PRIMARY KEY (supplier_no);
ALTER TABLE Supplier ADD CONSTRAINT city_check CHECK (city IN ('Pune','Mumbai','Nashik'));
ALTER TABLE Supplier DROP COLUMN phone_no;
ALTER TABLE Supplier ALTER COLUMN supplier_name TYPE TEXT;
ALTER TABLE Supplier DROP CONSTRAINT city_check;

-- View the final schema before dropping:
\d Supplier
DROP TABLE Supplier;
```

## Notes / assumptions
The workbook asks to type `\d <table name>` in psql. `\d` is a psql meta-command, not standard SQL.
