# Assignment 3 – Set A – Q2: Student ALTER/DROP Exercise

## Lab-book task
Create Student and execute the requested ALTER/DROP sequence, including rename and column changes.

## Solution
```sql
DROP TABLE IF EXISTS Student CASCADE;
CREATE TABLE Student (
    stud_no INTEGER,
    stud_name VARCHAR(50),
    address CHAR(10),
    phone_no BIGINT,
    percentage DOUBLE PRECISION,
    class VARCHAR(10)
);
ALTER TABLE Student ADD CONSTRAINT student_pk PRIMARY KEY (stud_no);
ALTER TABLE Student ADD CONSTRAINT per_check CHECK (percentage > 35);
ALTER TABLE Student RENAME COLUMN phone_no TO mobile_no;
ALTER TABLE Student ALTER COLUMN stud_name TYPE TEXT;
ALTER TABLE Student RENAME TO Student_Master;
ALTER TABLE Student_Master DROP COLUMN address;
\d Student_Master
DROP TABLE Student_Master;

-- The workbook also asks to remove employee table:
DROP TABLE IF EXISTS Employee CASCADE;
```
