# Assignment 3 – Set C – Q1: Client–Sales Order DML

## Lab-book task
Create Client and Sales_order for one-to-many Client→Sales_order, insert 2 clients and 3 orders per client, update/delete as specified.

## Solution
```sql
DROP TABLE IF EXISTS Sales_order CASCADE;
DROP TABLE IF EXISTS Client CASCADE;
CREATE TABLE Client(
    client_no VARCHAR(10) PRIMARY KEY,
    name VARCHAR(50),
    address VARCHAR(100)
);
CREATE TABLE Sales_order(
    s_order_no INTEGER PRIMARY KEY,
    s_order_date DATE NOT NULL,
    client_no VARCHAR(10) NOT NULL REFERENCES Client(client_no)
);
INSERT INTO Client VALUES
('C004','Riya','Pune'),('C005','Amit','Mumbai');
INSERT INTO Sales_order VALUES
(101,DATE '2024-08-01','C004'),(102,DATE '2024-10-15','C004'),(103,DATE '2025-01-10','C004'),
(104,DATE '2024-07-20','C005'),(105,DATE '2024-11-01','C005'),(106,DATE '2025-02-12','C005');
UPDATE Sales_order SET s_order_date = DATE '2025-06-12' WHERE client_no='C004';
DELETE FROM Sales_order WHERE s_order_date < DATE '2024-09-10';
DELETE FROM Client WHERE address = 'Mumbai';
```

## Notes / assumptions
The final client deletion succeeds because its related sales orders with dates before 2024-09-10 are deleted first; remaining orders for C005 are still present, so if the instructor’s PostgreSQL FK rejects the delete, delete the client’s remaining orders first or use `ON DELETE CASCADE` as an explicitly chosen design.
