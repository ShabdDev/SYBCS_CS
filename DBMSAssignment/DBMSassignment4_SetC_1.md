# Assignment 4 – Set C – Sailors, Boats, Reserves

## Lab-book task
Create Sailors, Boats and Reserves in 3NF with 5 records each, then solve the three queries.

## Solution
### PostgreSQL solution

```sql
DROP TABLE IF EXISTS Reserves CASCADE;
DROP TABLE IF EXISTS Boats CASCADE;
DROP TABLE IF EXISTS Sailors CASCADE;

CREATE TABLE Sailors(sid INTEGER PRIMARY KEY, sname VARCHAR(50), rate INTEGER, age INTEGER);
CREATE TABLE Boats(bid INTEGER PRIMARY KEY, bname VARCHAR(50), colour VARCHAR(20));
CREATE TABLE Reserves(
    sid INTEGER REFERENCES Sailors(sid),
    bid INTEGER REFERENCES Boats(bid),
    date DATE,
    PRIMARY KEY(sid,bid,date)
);

INSERT INTO Sailors VALUES
(1,'Paul',9,25),(2,'Peter',7,30),(3,'Pranav',10,28),(4,'Suresh',8,35),(5,'Pooja',6,22);
INSERT INTO Boats VALUES
(1,'BoatA','red'),(2,'BoatB','green'),(3,'BoatC','blue'),(4,'BoatD','red'),(5,'BoatE','green');
INSERT INTO Reserves VALUES
(1,1,'2024-01-10'),(1,2,'2024-01-11'),(2,3,'2024-01-12'),(3,4,'2024-01-13'),(4,5,'2024-01-14');

SELECT * FROM Sailors WHERE rate > 8;
SELECT age FROM Sailors WHERE sname LIKE 'P%P';
SELECT s.sname
FROM Sailors s
JOIN Reserves r ON r.sid=s.sid
JOIN Boats b ON b.bid=r.bid
WHERE b.colour IN ('red','green')
GROUP BY s.sid,s.sname
HAVING COUNT(DISTINCT b.colour)=2;
```

For the ER diagram: Sailors and Boats are entities; Reserves is the associative entity for their M:N relationship, with `date` as a descriptive attribute. This removes the M:N relationship into two 1:M relationships and gives the normalized 3NF design.
