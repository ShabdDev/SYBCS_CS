# Assignment 6 – Set B – Employee-Project Nested Queries

## Lab-book task
Create Emp, Project and Emp_Project in 3NF and solve the six nested-query/EXISTS tasks.

## Solution
```sql
DROP TABLE IF EXISTS Emp_Project CASCADE;
DROP TABLE IF EXISTS Project CASCADE;
DROP TABLE IF EXISTS Emp CASCADE;
DROP TABLE IF EXISTS Department CASCADE;
CREATE TABLE Department(dno INTEGER PRIMARY KEY,dname VARCHAR(50));
CREATE TABLE Emp(eno INTEGER PRIMARY KEY,name VARCHAR(50),dno INTEGER REFERENCES Department(dno),salary NUMERIC(12,2));
CREATE TABLE Project(pno INTEGER PRIMARY KEY,pname VARCHAR(50),control_dno INTEGER REFERENCES Department(dno),budget NUMERIC(14,2));
CREATE TABLE Emp_Project(eno INTEGER REFERENCES Emp(eno),pno INTEGER REFERENCES Project(pno),hours NUMERIC(8,2),PRIMARY KEY(eno,pno));
INSERT INTO Department VALUES(10,'IT'),(20,'Sales'),(30,'HR');
INSERT INTO Emp VALUES(1,'Asha',10,80000),(2,'Ravi',10,70000),(3,'Neha',20,65000),(4,'Amit',20,75000),(5,'Kiran',30,60000);
INSERT INTO Project VALUES(101,'ERP',10,900000),(102,'Sales',20,500000),(103,'HRMS',30,300000),(104,'CRM',20,600000);
INSERT INTO Emp_Project VALUES(1,101,20),(1,104,30),(2,101,15),(3,102,40),(4,102,20),(4,104,10),(5,103,25);

-- Replace employee name <X> with the employee named in your lab question.
-- 1. Employees who work on all projects that X works on.
SELECT e.name FROM Emp e WHERE e.eno<>1 AND NOT EXISTS (
  SELECT 1 FROM Emp_Project x WHERE x.eno=1
  AND NOT EXISTS (SELECT 1 FROM Emp_Project y WHERE y.eno=e.eno AND y.pno=x.pno)
);
-- 2. Employees who work on only some projects X works on (at least one common, but not all).
SELECT e.name FROM Emp e WHERE e.eno<>1
AND EXISTS (SELECT 1 FROM Emp_Project x JOIN Emp_Project y ON y.pno=x.pno WHERE x.eno=1 AND y.eno=e.eno)
AND EXISTS (SELECT 1 FROM Emp_Project x WHERE x.eno=1 AND NOT EXISTS (SELECT 1 FROM Emp_Project y WHERE y.eno=e.eno AND y.pno=x.pno));
-- 3. Departments having at least one project: EXISTS.
SELECT d.dname FROM Department d WHERE EXISTS (SELECT 1 FROM Project p WHERE p.control_dno=d.dno);
-- 4. Employees who do not work on Sales project: NOT EXISTS.
SELECT e.name FROM Emp e WHERE NOT EXISTS (SELECT 1 FROM Emp_Project ep JOIN Project p ON p.pno=ep.pno WHERE ep.eno=e.eno AND LOWER(p.pname)='sales');
-- 5. Employees who work only on projects controlled by their department.
SELECT e.name FROM Emp e WHERE EXISTS (SELECT 1 FROM Emp_Project ep WHERE ep.eno=e.eno)
AND NOT EXISTS (SELECT 1 FROM Emp_Project ep JOIN Project p ON p.pno=ep.pno WHERE ep.eno=e.eno AND p.control_dno<>e.dno);
-- 6. Employees who do not work on any project controlled by their department.
SELECT e.name FROM Emp e WHERE NOT EXISTS (SELECT 1 FROM Emp_Project ep JOIN Project p ON p.pno=ep.pno WHERE ep.eno=e.eno AND p.control_dno=e.dno);
```

## Notes / assumptions
The first two queries use employee 1 as the concrete example because the workbook leaves the employee name blank. Replace `1` with the appropriate employee number after identifying the named employee.
