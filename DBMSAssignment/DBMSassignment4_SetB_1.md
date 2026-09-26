# Assignment 4 – Set B – Competition Queries

## Lab-book task
Create Competition(C_no, Name, Type, No_of_participants, cdate, budget) and solve all 10 queries.

## Solution
```sql
DROP TABLE IF EXISTS Competition CASCADE;
CREATE TABLE Competition(
    c_no INTEGER PRIMARY KEY,
    name CHAR(20),
    type CHAR(15),
    no_of_participants INTEGER,
    cdate DATE,
    budget DOUBLE PRECISION
);
INSERT INTO Competition VALUES
(1,'Quiz','Academic',50,'2024-01-15',10000),(2,'Cricket','Sports',100,'2024-02-20',50000),
(3,'Debate','Academic',30,'2023-08-10',8000),(4,'Football','Sports',120,'2024-09-05',60000),
(5,'Coding','Academic',70,'2024-11-11',20000),(6,'Athletics','Sports',150,'2023-12-01',40000);
SELECT * FROM Competition;
SELECT name FROM Competition WHERE EXTRACT(YEAR FROM cdate)=2024;
SELECT name FROM Competition WHERE TRIM(LOWER(type))='academic';
SELECT COUNT(*) FROM Competition WHERE TRIM(LOWER(type))='sports';
SELECT MAX(no_of_participants) FROM Competition;
SELECT AVG(budget) FROM Competition WHERE TRIM(LOWER(type))='sports';
SELECT name FROM Competition WHERE no_of_participants=(SELECT MAX(no_of_participants) FROM Competition);
SELECT name FROM Competition WHERE budget=(SELECT MIN(budget) FROM Competition);
SELECT TRIM(type) AS type, COUNT(*) FROM Competition GROUP BY TRIM(type);
SELECT TRIM(type) AS type, SUM(budget) FROM Competition GROUP BY TRIM(type);
```
