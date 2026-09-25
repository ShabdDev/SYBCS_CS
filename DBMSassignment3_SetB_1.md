# Assignment 3 – Set B – Q1: Supplier and Student DML

## Lab-book task
Create Supplier and Student with constraints, insert 5 records each, then execute the requested updates/deletes.

## Solution
```sql
DROP TABLE IF EXISTS Supplier CASCADE;
DROP TABLE IF EXISTS Student CASCADE;
CREATE TABLE Supplier(
    supplier_no INTEGER PRIMARY KEY,
    supplier_name VARCHAR(50),
    city CHAR(10),
    phone_no BIGINT,
    bill_amount DOUBLE PRECISION CHECK (bill_amount > 0),
    CONSTRAINT city_check CHECK (city IN ('Pune','Mumbai','Nashik'))
);
CREATE TABLE Student(
    stud_no INTEGER PRIMARY KEY,
    stud_name VARCHAR(50),
    address CHAR(10),
    phone_no BIGINT,
    percentage DOUBLE PRECISION,
    class VARCHAR(10),
    CONSTRAINT class_check CHECK (class IN ('FY','SY','TY'))
);
INSERT INTO Supplier VALUES
(1,'ABC','Pune',1111111111,10000),(2,'XYZ','Mumbai',2222222222,12000),
(3,'PQR','Nashik',3333333333,9000),(4,'LMN','Pune',4444444444,15000),(5,'DEF','Mumbai',5555555555,8000);
INSERT INTO Student VALUES
(1,'Amit','Pune',1111111111,42,'FY'),(2,'Neha','Pune',2222222222,55,'SY'),
(3,'Riya','Nashik',3333333333,38,'FY'),(4,'Sonal','Mumbai',4444444444,67,'TY'),(5,'Vijay','Pune',5555555555,35,'SY');

UPDATE Supplier SET bill_amount = bill_amount * 1.05;
UPDATE Supplier SET city = 'Nagpur' WHERE city = 'Nashik';
-- The original city_check constraint must be removed before the previous update can succeed.
ALTER TABLE Supplier DROP CONSTRAINT city_check;
UPDATE Student SET percentage = percentage + 3 WHERE class = 'FY';
DELETE FROM Supplier WHERE city = 'Mumbai';
DELETE FROM Student WHERE percentage < 40;
```

## Notes / assumptions
Because the original Set B constraint allows only Pune/Mumbai/Nashik, changing Nashik to Nagpur requires dropping or changing `city_check` first. The workbook asks for the update, so the solution explicitly removes that constraint before performing it.
