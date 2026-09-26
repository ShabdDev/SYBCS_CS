# Assignment 2 – Set A – Q3: Patient–Bed One-to-One

## Lab-book task
Create Patient and Bed for a one-to-one relationship.

## Solution
```sql
DROP TABLE IF EXISTS Bed CASCADE;
DROP TABLE IF EXISTS Patient CASCADE;
CREATE TABLE Patient (
    pno INTEGER PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    address VARCHAR(50)
);
CREATE TABLE Bed (
    bedno INTEGER,
    roomno INTEGER,
    description VARCHAR(50),
    pno INTEGER UNIQUE REFERENCES Patient(pno),
    PRIMARY KEY (bedno,roomno)
);
```

## Notes / assumptions
A UNIQUE foreign key on Bed.pno ensures that one patient is linked to at most one bed. If every bed must be assigned, add NOT NULL as well.
