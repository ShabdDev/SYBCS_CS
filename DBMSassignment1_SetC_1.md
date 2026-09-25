# Assignment 1 – Set C – Student Table

## Lab-book task
Create Student with primary key, uppercase non-null name, class in FY/SY/TY, positive marks, unique UID, and UID different from ID.

## Solution
```sql
DROP TABLE IF EXISTS Student CASCADE;
CREATE TABLE Student (
    stud_id    INTEGER PRIMARY KEY,
    stud_name  VARCHAR(50) NOT NULL,
    stud_class VARCHAR(10),
    stud_marks DOUBLE PRECISION,
    stud_uid   TEXT UNIQUE,
    CONSTRAINT stud_name_upper CHECK (stud_name = UPPER(stud_name)),
    CONSTRAINT stud_class_chk CHECK (stud_class IN ('FY','SY','TY')),
    CONSTRAINT stud_marks_chk CHECK (stud_marks > 0),
    CONSTRAINT stud_uid_diff CHECK (stud_uid <> stud_id::TEXT)
);
```
