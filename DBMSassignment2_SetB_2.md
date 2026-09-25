# Assignment 2 – Set B – Q2: Project–Employee Many-to-Many

## Lab-book task
Create Project and Employee plus a junction relation with Start date and no_of_hours_worked.

## Solution
```sql
DROP TABLE IF EXISTS Project_Employee CASCADE;
DROP TABLE IF EXISTS Project CASCADE;
DROP TABLE IF EXISTS Employee CASCADE;
CREATE TABLE Project (
    pno INTEGER PRIMARY KEY,
    pname VARCHAR(30) NOT NULL,
    ptype CHAR(20),
    duration INTEGER
);
CREATE TABLE Employee (
    eno INTEGER PRIMARY KEY,
    ename VARCHAR(20),
    qualification VARCHAR(50),
    join_date DATE,
    salary DOUBLE PRECISION CHECK (salary > 0)
);
CREATE TABLE Project_Employee (
    pno INTEGER REFERENCES Project(pno),
    eno INTEGER REFERENCES Employee(eno),
    start_date DATE,
    no_of_hours_worked INTEGER,
    PRIMARY KEY (pno,eno)
);
```
