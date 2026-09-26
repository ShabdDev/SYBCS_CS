# Assignment 5 – Set A – Q1: Investment Firm Set Operations

## Lab-book task
Create Emp and Investor with a relationship where an employee may be an investor but an investor need not be an employee, then solve four set-operation queries.

## Solution
```sql
DROP TABLE IF EXISTS Investor CASCADE;
DROP TABLE IF EXISTS Emp CASCADE;
CREATE TABLE Emp(
    emp_id INTEGER PRIMARY KEY,
    emp_name VARCHAR(50),
    address VARCHAR(100),
    bdate DATE
);
CREATE TABLE Investor(
    inv_no INTEGER PRIMARY KEY,
    inv_name VARCHAR(50),
    inv_date DATE,
    inv_amt NUMERIC(12,2),
    emp_id INTEGER REFERENCES Emp(emp_id)
);
INSERT INTO Emp VALUES
(1,'Asha','Pune','1998-01-01'),(2,'Ravi','Mumbai','1997-02-02'),(3,'Neha','Pune','1999-03-03'),(4,'Amit','Delhi','1996-04-04');
INSERT INTO Investor VALUES
(101,'Asha','2025-01-01',50000,1),(102,'Ravi','2025-01-02',60000,2),(103,'Kiran','2025-01-03',70000,NULL),(104,'Neha','2025-01-04',45000,3);

-- 1. Distinct names: UNION removes duplicates.
SELECT emp_name AS customer_name FROM Emp
UNION
SELECT inv_name FROM Investor;

-- 2. Names of all customers, retaining duplicates.
SELECT emp_name AS customer_name FROM Emp
UNION ALL
SELECT inv_name FROM Investor;

-- 3. Employees who are also investors.
SELECT emp_name AS customer_name FROM Emp
INTERSECT
SELECT inv_name FROM Investor;

-- 4. Employees who are not investors.
SELECT emp_name AS customer_name FROM Emp
EXCEPT
SELECT inv_name FROM Investor;
```
