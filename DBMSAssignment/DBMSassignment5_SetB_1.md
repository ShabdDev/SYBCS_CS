# Assignment 5 – Set B – Q1: Employee/Project/Department Set Operations and DML

## Lab-book task
Create normalized Employee, Project, Department and bridge relations; solve the three workbook queries.

## Solution
```sql
DROP TABLE IF EXISTS Employee_Project CASCADE;
DROP TABLE IF EXISTS Employee CASCADE;
DROP TABLE IF EXISTS Project CASCADE;
DROP TABLE IF EXISTS Department CASCADE;
CREATE TABLE Department(dept_no INTEGER PRIMARY KEY,dept_name VARCHAR(50),location VARCHAR(50));
CREATE TABLE Employee(emp_no INTEGER PRIMARY KEY,emp_name VARCHAR(50),address VARCHAR(100),city VARCHAR(50),birth_date DATE,designation VARCHAR(20) CHECK(designation IN ('manager','staff','worker')),salary NUMERIC(12,2),dept_no INTEGER REFERENCES Department(dept_no));
CREATE TABLE Project(project_no INTEGER PRIMARY KEY,project_name VARCHAR(50),status VARCHAR(30),control_dept_no INTEGER REFERENCES Department(dept_no));
CREATE TABLE Employee_Project(emp_no INTEGER REFERENCES Employee(emp_no),project_no INTEGER REFERENCES Project(project_no),PRIMARY KEY(emp_no,project_no));
INSERT INTO Department VALUES(10,'IT','Pune'),(20,'Sales','Mumbai'),(30,'HR','Delhi'),(40,'Accounts','Nashik'),(50,'Research','Pune');
INSERT INTO Employee VALUES
(1,'Asha','Pune','Pune','1998-01-01','manager',70000,10),(2,'Ravi','Mumbai','Mumbai','1997-02-02','staff',50000,20),(3,'Neha','Pune','Pune','1999-03-03','worker',45000,10),(4,'Amit','Delhi','Delhi','1996-04-04','manager',80000,30),(5,'Kiran','Nashik','Nashik','1995-05-05','staff',55000,40);
INSERT INTO Project VALUES(101,'ERP','active',10),(102,'CRM','active',20),(103,'Payroll','active',30),(104,'Website','active',10),(105,'Audit','active',40);
INSERT INTO Employee_Project VALUES(1,101),(1,104),(2,102),(3,101),(4,103),(5,105);

SELECT * FROM Employee WHERE salary=(SELECT MAX(salary) FROM Employee);
DELETE FROM Employee WHERE dept_no=20;
SELECT emp_name,salary FROM Employee ORDER BY salary;
```

## Notes / assumptions
The workbook asks for “many employees can work on many projects controlled by a department”; the bridge table represents that M:N relationship. Deleting department-20 employees may require deleting their bridge rows first in PostgreSQL if foreign keys are not defined with ON DELETE CASCADE.
