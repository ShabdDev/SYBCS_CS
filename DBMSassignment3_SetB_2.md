# Assignment 3 – Set B – Q2: Department–Employee DML

## Lab-book task
Create Department and Emp with a one-to-many relationship, insert 5 departments and 2 employees per department, then perform the requested DML.

## Solution
```sql
DROP TABLE IF EXISTS Emp CASCADE;
DROP TABLE IF EXISTS Dept CASCADE;
CREATE TABLE Dept(
    dno INTEGER PRIMARY KEY,
    dname VARCHAR(30),
    dloc VARCHAR(30)
);
CREATE TABLE Emp(
    eno INTEGER PRIMARY KEY,
    ename VARCHAR(50),
    designation VARCHAR(30),
    sal DOUBLE PRECISION,
    dno INTEGER REFERENCES Dept(dno)
);
INSERT INTO Dept VALUES
(10,'Research','Pune'),(20,'Sales','Mumbai'),(30,'Accounts','Pune'),(40,'HR','Delhi'),(50,'IT','Nashik');
INSERT INTO Emp VALUES
(1,'Asha','manager',50000,10),(2,'Ravi','clerk',25000,10),
(3,'Neha','manager',52000,20),(4,'Amit','clerk',24000,20),
(5,'Pooja','manager',55000,30),(6,'Vijay','clerk',26000,30),
(7,'Kiran','staff',35000,40),(8,'Sonal','clerk',23000,40),
(9,'Rohit','manager',60000,50),(10,'Meena','clerk',27000,50);

UPDATE Emp SET sal = sal * 1.15 WHERE LOWER(designation) = 'manager';
DELETE FROM Emp WHERE dno = 30;
DELETE FROM Emp WHERE LOWER(designation) = 'clerk';
UPDATE Dept SET dloc = 'Nashik' WHERE dname = 'Account' OR dname = 'Accounts';
```
