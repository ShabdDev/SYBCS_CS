# Assignment 1 – Set A – Q2: Student Table

## Lab-book task
Create Student(Roll_no, Class, Weight, Height) with composite primary key (Roll_no, Class).

## Solution
```sql
DROP TABLE IF EXISTS Student CASCADE;
CREATE TABLE Student (
    roll_no INTEGER,
    class   VARCHAR(20),
    weight  NUMERIC(6,2),
    height  NUMERIC(6,2),
    CONSTRAINT student_pk PRIMARY KEY (roll_no, class)
);

INSERT INTO Student VALUES
(1,'SY',55.20,165.50),
(1,'TY',58.00,166.00);
SELECT * FROM Student;
```
