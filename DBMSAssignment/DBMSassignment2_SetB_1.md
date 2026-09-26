# Assignment 2 – Set B – Q1: Student–Teacher Many-to-Many with Marks

## Lab-book task
Create Student, Teacher and a junction relation containing descriptive attribute Marks.

## Solution
```sql
DROP TABLE IF EXISTS Student_Teacher CASCADE;
DROP TABLE IF EXISTS Teacher CASCADE;
DROP TABLE IF EXISTS Student CASCADE;
CREATE TABLE Student (
    sno INTEGER PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    address VARCHAR(50),
    class VARCHAR(10)
);
CREATE TABLE Teacher (
    tno INTEGER PRIMARY KEY,
    tname VARCHAR(50) NOT NULL,
    qualification VARCHAR(50),
    totalexperience DOUBLE PRECISION,
    salary DOUBLE PRECISION CHECK (salary > 0)
);
CREATE TABLE Student_Teacher (
    sno INTEGER REFERENCES Student(sno),
    tno INTEGER REFERENCES Teacher(tno),
    marks DOUBLE PRECISION,
    PRIMARY KEY (sno,tno)
);
```

## Notes / assumptions
The workbook lists Tname as integer primary key in its table, but that conflicts with the field name and the intended teacher entity. The solution uses `tno` as the teacher primary key and `tname` as text, preserving the relationship semantics.
