# Assignment 6 – Set B – Bank Database Nested Queries and Views

## Lab-book task
Create Branch, Customer, Loan_Application and ternary relationship, then solve the six bank queries and view tasks.

## Solution
```sql
DROP TABLE IF EXISTS Ternary CASCADE;
DROP TABLE IF EXISTS Loan_Application CASCADE;
DROP TABLE IF EXISTS Customer CASCADE;
DROP TABLE IF EXISTS Branch CASCADE;
CREATE TABLE Branch(bid INTEGER PRIMARY KEY,brname CHAR(30),brcity CHAR(10));
CREATE TABLE Customer(cno INTEGER PRIMARY KEY,cname CHAR(20),caddr CHAR(35),city VARCHAR(20));
CREATE TABLE Loan_Application(lno INTEGER PRIMARY KEY,lamtrequired NUMERIC(14,2),lamtapproved NUMERIC(14,2),l_date DATE);
CREATE TABLE Ternary(bid INTEGER REFERENCES Branch(bid),cno INTEGER REFERENCES Customer(cno),lno INTEGER REFERENCES Loan_Application(lno),PRIMARY KEY(bid,cno,lno));
INSERT INTO Branch VALUES(1,'Aundh','Pune'),(2,'Deccan','Pune'),(3,'M.G. ROAD','Pune');
INSERT INTO Customer VALUES(1,'Asha','Addr1','Pune'),(2,'Ravi','Addr2','Mumbai'),(3,'Neha','Addr3','Pune'),(4,'Amit','Addr4','Delhi');
INSERT INTO Loan_Application VALUES(101,500000,450000,'2019-09-10'),(102,300000,300000,'2019-09-15'),(103,800000,600000,'2020-01-10'),(104,900000,700000,'2020-06-01');
INSERT INTO Ternary VALUES(1,1,101),(2,2,102),(2,3,103),(3,4,104);

SELECT DISTINCT c.cname FROM Customer c JOIN Ternary t ON t.cno=c.cno JOIN Branch b ON b.bid=t.bid WHERE TRIM(b.brname)='Aundh';
SELECT DISTINCT c.cname FROM Customer c JOIN Ternary t ON t.cno=c.cno JOIN Loan_Application l ON l.lno=t.lno WHERE l.lamtapproved<l.lamtrequired;
SELECT MAX(lamtapproved) FROM Loan_Application;
SELECT SUM(l.lamtapproved) FROM Loan_Application l JOIN Ternary t ON t.lno=l.lno JOIN Branch b ON b.bid=t.bid WHERE TRIM(b.brname)='Deccan';
SELECT COUNT(DISTINCT t.lno) FROM Ternary t JOIN Branch b ON b.bid=t.bid WHERE TRIM(b.brname)='M.G. ROAD';
SELECT DISTINCT c.cname,TRIM(b.brname) AS branch_name FROM Customer c JOIN Ternary t ON t.cno=c.cno JOIN Branch b ON b.bid=t.bid JOIN Loan_Application l ON l.lno=t.lno WHERE EXTRACT(MONTH FROM l.l_date)=9;

CREATE OR REPLACE VIEW v_less_than_required AS
SELECT c.*,l.lamtrequired,l.lamtapproved FROM Customer c JOIN Ternary t ON t.cno=c.cno JOIN Loan_Application l ON l.lno=t.lno WHERE l.lamtapproved<l.lamtrequired;
CREATE OR REPLACE VIEW v_branch_sum_2019_2020 AS
SELECT b.brname,SUM(l.lamtapproved) AS total_approved FROM Branch b JOIN Ternary t ON t.bid=b.bid JOIN Loan_Application l ON l.lno=t.lno WHERE l.l_date BETWEEN DATE '2019-06-01' AND DATE '2020-06-01' GROUP BY b.brname;
-- Count branch-wise customers requiring more than 30 lakhs.
SELECT TRIM(b.brname),COUNT(DISTINCT c.cno) FROM Branch b JOIN Ternary t ON t.bid=b.bid JOIN Customer c ON c.cno=t.cno JOIN Loan_Application l ON l.lno=t.lno WHERE l.lamtrequired>3000000 GROUP BY b.brname;
-- Customer names branch-wise requesting less than one lakh.
SELECT TRIM(b.brname),c.cname FROM Branch b JOIN Ternary t ON t.bid=b.bid JOIN Customer c ON c.cno=t.cno JOIN Loan_Application l ON l.lno=t.lno WHERE l.lamtrequired<100000;
```
