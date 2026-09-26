# Assignment 6 – Set A – Employee/Project Nested Queries and Views

## Lab-book task
Create Emp, Project and a work-assignment bridge in 3NF and solve the 12 nested-query business tasks plus the 5 views.

## Solution
```sql
DROP TABLE IF EXISTS Emp_Project CASCADE;
DROP TABLE IF EXISTS Project CASCADE;
DROP TABLE IF EXISTS Emp CASCADE;
DROP TABLE IF EXISTS Department CASCADE;
CREATE TABLE Department(dno INTEGER PRIMARY KEY,dname VARCHAR(50));
CREATE TABLE Emp(eno INTEGER PRIMARY KEY,name VARCHAR(50),dno INTEGER REFERENCES Department(dno),salary NUMERIC(12,2),gender CHAR(1),address VARCHAR(100),qualification VARCHAR(20));
CREATE TABLE Project(pno INTEGER PRIMARY KEY,pname VARCHAR(50),control_dno INTEGER REFERENCES Department(dno),budget NUMERIC(14,2),start_date DATE);
CREATE TABLE Emp_Project(eno INTEGER REFERENCES Emp(eno),pno INTEGER REFERENCES Project(pno),hours NUMERIC(8,2),PRIMARY KEY(eno,pno));
INSERT INTO Department VALUES(10,'IT'),(20,'Sales'),(30,'HR'),(40,'Accounts');
INSERT INTO Emp VALUES
(1,'Asha',10,80000,'F','Pune','MCA'),(2,'Ravi',10,75000,'M','Mumbai','BCA'),(3,'Neha',20,70000,'F','Pune','MCA'),
(4,'Amit',20,90000,'M','Delhi','MCA'),(5,'Kiran',30,60000,'M','Nashik','BSc'),(6,'Sonal',40,65000,'F','Pune','MCA');
INSERT INTO Project VALUES
(101,'ERP',10,900000,'2025-01-01'),(102,'CRM',20,500000,'2025-03-01'),(103,'HRMS',30,300000,'2025-02-01'),(104,'Website',10,700000,'2024-01-01');
INSERT INTO Emp_Project VALUES(1,101,320),(1,104,50),(2,101,20),(2,104,80),(3,102,40),(4,102,60),(5,103,15),(6,104,310);

-- 1. Departments controlling projects over a budget threshold.
SELECT DISTINCT d.dname FROM Department d JOIN Project p ON p.control_dno=d.dno WHERE p.budget > 600000;
-- 2. Projects controlled by one department whose budget exceeds at least one project of another department.
SELECT p.pname FROM Project p WHERE p.control_dno=10 AND p.budget > ANY (SELECT p2.budget FROM Project p2 WHERE p2.control_dno=20);
-- 3. Projects with second maximum budget.
SELECT * FROM Project WHERE budget=(SELECT MAX(budget) FROM Project WHERE budget < (SELECT MAX(budget) FROM Project));
-- 5. Employees sharing at least one project with employee 1.
SELECT DISTINCT e.name FROM Emp e JOIN Emp_Project ep ON ep.eno=e.eno WHERE ep.pno IN (SELECT pno FROM Emp_Project WHERE eno=1) AND e.eno<>1;
-- 6. Employees sharing none of employee 1's projects.
SELECT e.name FROM Emp e WHERE e.eno<>1 AND NOT EXISTS (SELECT 1 FROM Emp_Project ep WHERE ep.eno=e.eno AND ep.pno IN (SELECT pno FROM Emp_Project WHERE eno=1));
-- 7. Employees who work on no project controlled by department named Sales.
SELECT e.name FROM Emp e WHERE NOT EXISTS (SELECT 1 FROM Emp_Project ep JOIN Project p ON p.pno=ep.pno JOIN Department d ON d.dno=p.control_dno WHERE ep.eno=e.eno AND d.dname='Sales');
-- 8. Projects with at least 2 employees.
SELECT p.pname,d.dname FROM Project p JOIN Department d ON d.dno=p.control_dno WHERE (SELECT COUNT(*) FROM Emp_Project ep WHERE ep.pno=p.pno)>=2;
-- 9. Employees with >10 hours on at least one project controlled by IT.
SELECT DISTINCT e.name FROM Emp e JOIN Emp_Project ep ON ep.eno=e.eno JOIN Project p ON p.pno=ep.pno JOIN Department d ON d.dno=p.control_dno WHERE ep.hours>10 AND d.dname='IT';
-- 10. Male employees with maximum salary in their department.
SELECT e.name FROM Emp e WHERE e.gender='M' AND e.salary=(SELECT MAX(e2.salary) FROM Emp e2 WHERE e2.dno=e.dno);
-- 11. Employees in same department as Asha.
SELECT name FROM Emp WHERE dno=(SELECT dno FROM Emp WHERE name='Asha');
-- 12. Employees not living in two specified cities.
SELECT name FROM Emp WHERE address NOT IN ('Pune','Mumbai');

CREATE OR REPLACE VIEW v_erp_employees AS
SELECT e.* FROM Emp e JOIN Emp_Project ep ON ep.eno=e.eno JOIN Project p ON p.pno=ep.pno WHERE p.pname='ERP';
CREATE OR REPLACE VIEW v_long_projects AS
SELECT p.* FROM Project p WHERE p.start_date <= CURRENT_DATE - INTERVAL '6 months' ORDER BY p.start_date;
CREATE OR REPLACE VIEW v_mca_employees AS SELECT * FROM Emp WHERE qualification='MCA';
CREATE OR REPLACE VIEW v_employee_project_300h AS
SELECT e.name AS employee_name,p.pname AS project_name,ep.hours FROM Emp e JOIN Emp_Project ep ON ep.eno=e.eno JOIN Project p ON p.pno=ep.pno WHERE ep.hours>300;
DROP VIEW IF EXISTS v_mca_employees;
```

## Notes / assumptions
The workbook uses blanks such as department number, employee number, threshold, department name, and city names. The solution supplies concrete sample values where needed and shows the corresponding query pattern; replace them with your instructor’s assigned values.
