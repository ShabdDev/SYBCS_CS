# Assignment 2 – Set A – Q2: Hospital–Doctor Many-to-Many

## Lab-book task
Create Hospital and Doctor plus a junction relation for their many-to-many relationship.

## Solution
```sql
DROP TABLE IF EXISTS Hospital_Doctor CASCADE;
DROP TABLE IF EXISTS Doctor CASCADE;
DROP TABLE IF EXISTS Hospital CASCADE;
CREATE TABLE Hospital (
    hno INTEGER PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    city CHAR(10)
);
CREATE TABLE Doctor (
    dno INTEGER PRIMARY KEY,
    dname VARCHAR(50),
    city CHAR(10)
);
CREATE TABLE Hospital_Doctor (
    hno INTEGER REFERENCES Hospital(hno),
    dno INTEGER REFERENCES Doctor(dno),
    PRIMARY KEY (hno,dno)
);
```
