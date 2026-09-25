# Assignment 4 – Set A – Q1: Employee Simple Queries

## Lab-book task
Create Employee(empno,name,age,address,salary,deptno), insert at least 10 records, and execute the 12 workbook queries.

## Solution
```sql
DROP TABLE IF EXISTS Employee CASCADE;
CREATE TABLE Employee(
    empno INTEGER PRIMARY KEY,
    name VARCHAR(50),
    age INTEGER,
    address VARCHAR(100),
    salary NUMERIC(12,2),
    deptno INTEGER
);
INSERT INTO Employee VALUES
(1,'Sonal',28,'Pune',55000,5),(2,'Amit',32,'Mumbai',48000,5),(3,'Sunil',26,'Pune',62000,10),
(4,'Rina',36,'Nashik',70000,10),(5,'Nitin',30,'Pune',52000,5),(6,'Kiran',24,'Mumbai',45000,20),
(7,'Suresh',40,'Pune',90000,20),(8,'Anita',29,'Delhi',58000,10),(9,'Sanjay',34,'Pune',61000,5),(10,'Neha',27,'Pune',50000,20);

SELECT * FROM Employee;
SELECT DISTINCT deptno FROM Employee;
SELECT * FROM Employee WHERE deptno = 5;
SELECT * FROM Employee WHERE address = 'Pune' AND salary > 50000;
SELECT * FROM Employee WHERE age BETWEEN 25 AND 35;
SELECT empno,name FROM Employee WHERE name LIKE 'S%';
SELECT * FROM Employee WHERE name ILIKE '%nit%';
SELECT MAX(salary) AS max_salary FROM Employee;
SELECT AVG(salary) AS avg_salary FROM Employee;
SELECT COUNT(*) AS count_age_less_35 FROM Employee WHERE age < 35;
SELECT SUM(salary) AS total_salary_expenditure FROM Employee;
SELECT deptno, COUNT(*) AS employee_count FROM Employee GROUP BY deptno ORDER BY deptno;
```
