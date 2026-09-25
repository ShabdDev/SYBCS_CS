# Assignment 6 – Set C – Student–Teacher Nested Queries

## Lab-book task
Create Student, Teacher and a Student_Teacher M:N relation with Subject, then solve all six queries.

## Solution
```sql
DROP TABLE IF EXISTS Student_Teacher CASCADE;
DROP TABLE IF EXISTS Teacher CASCADE;
DROP TABLE IF EXISTS Student CASCADE;
CREATE TABLE Student(sno INTEGER PRIMARY KEY,s_name CHAR(30),s_class CHAR(10),s_addr CHAR(50));
CREATE TABLE Teacher(tno INTEGER PRIMARY KEY,t_name CHAR(20),qualification CHAR(15),experience INTEGER);
CREATE TABLE Student_Teacher(sno INTEGER REFERENCES Student(sno),tno INTEGER REFERENCES Teacher(tno),subject VARCHAR(50),PRIMARY KEY(sno,tno,subject));
INSERT INTO Student VALUES(1,'Suresh','SY','Pune'),(2,'Amit','SY','Mumbai'),(3,'Neha','TY','Pune'),(4,'Riya','FY','Nashik'),(5,'Kiran','TY','Pune');
INSERT INTO Teacher VALUES(1,'Mr. Patil','MCA',10),(2,'Mrs. Joshi','Ph. D.',15),(3,'Mr. Shah','MSc',8),(4,'Ms. Wani','Ph. D.',12),(5,'Mr. Kale','MCA',5);
INSERT INTO Student_Teacher VALUES(1,1,'DBMS'),(1,2,'DS'),(2,1,'DBMS'),(3,2,'AI'),(4,3,'Maths'),(5,4,'Networks'),(3,1,'DS');

SELECT * FROM Teacher WHERE experience=(SELECT MIN(experience) FROM Teacher);
SELECT COUNT(*) FROM Teacher WHERE qualification='Ph. D.';
SELECT s.s_name,st.subject FROM Student s JOIN Student_Teacher st ON st.sno=s.sno JOIN Teacher t ON t.tno=st.tno WHERE TRIM(t.t_name)='Mr. Patil';
SELECT TRIM(t.t_name) AS teacher_name,st.subject FROM Teacher t JOIN Student_Teacher st ON st.tno=t.tno ORDER BY teacher_name,st.subject;
SELECT DISTINCT TRIM(t.t_name) FROM Teacher t JOIN Student_Teacher st ON st.tno=t.tno JOIN Student s ON s.sno=st.sno WHERE TRIM(s.s_name)='Suresh';
SELECT TRIM(t.t_name) AS teacher_name,COUNT(DISTINCT st.sno) AS total_students FROM Teacher t LEFT JOIN Student_Teacher st ON st.tno=t.tno GROUP BY t.tno,t.t_name ORDER BY teacher_name;
```
