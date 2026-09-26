# Assignment 2 – Set A – Q1: Owner–Property One-to-Many

## Lab-book task
Create Property and Owner tables for a one-to-many relationship between Owner and Property.

## Solution
```sql
DROP TABLE IF EXISTS Property CASCADE;
DROP TABLE IF EXISTS Owner CASCADE;
CREATE TABLE Owner (
    owner_name VARCHAR(50) PRIMARY KEY,
    address    VARCHAR(50),
    phoneno    BIGINT
);
CREATE TABLE Property (
    p_number   INTEGER PRIMARY KEY,
    description VARCHAR(50) NOT NULL,
    area       CHAR(10),
    owner_name VARCHAR(50) NOT NULL REFERENCES Owner(owner_name)
);
```

## Notes / assumptions
The one-side key Owner.owner_name is stored as a foreign key in Property, the many-side table.
