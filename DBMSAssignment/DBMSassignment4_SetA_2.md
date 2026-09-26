# Assignment 4 – Set A – Q2: Movie Database Queries

## Lab-book task
Normalize Movies, Actor and their many-to-many relationship into 3NF, insert records, and solve the 7 queries.

## Solution
```sql
DROP TABLE IF EXISTS Movie_Actor CASCADE;
DROP TABLE IF EXISTS Actor CASCADE;
DROP TABLE IF EXISTS Movies CASCADE;
CREATE TABLE Movies(
    movie_id SERIAL PRIMARY KEY,
    m_name VARCHAR(100) NOT NULL,
    release_year INTEGER,
    budget NUMERIC(14,2)
);
CREATE TABLE Actor(
    actor_id SERIAL PRIMARY KEY,
    a_name VARCHAR(100) NOT NULL,
    role VARCHAR(100),
    charges NUMERIC(14,2),
    a_address VARCHAR(100),
    age INTEGER
);
CREATE TABLE Movie_Actor(
    movie_id INTEGER REFERENCES Movies(movie_id),
    actor_id INTEGER REFERENCES Actor(actor_id),
    PRIMARY KEY(movie_id,actor_id)
);
INSERT INTO Movies(m_name,release_year,budget) VALUES
('Film One',2023,30000000),('Film Two',2024,50000000),('Film Three',2023,45000000),
('Film Four',2022,10000000),('Film Five',2023,60000000);
INSERT INTO Actor(a_name,role,charges,a_address,age) VALUES
('Arjun','Lead',250000,'Pune',30),('Kiran','Lead',180000,'Mumbai',34),('Mohan','Support',220000,'Delhi',40),
('Rohan','Lead',300000,'Pune',32),('Nitin','Support',150000,'Nashik',29),('Sanjay','Lead',350000,'Mumbai',42);
INSERT INTO Movie_Actor VALUES
(1,1),(1,2),(2,3),(2,4),(3,1),(3,5),(4,2),(5,4),(5,6);

SELECT a_name FROM Actor WHERE a_name LIKE '%n';
SELECT m_name FROM Movies WHERE budget = (SELECT MAX(budget) FROM Movies);
SELECT a_name FROM Actor WHERE charges > 200000;
SELECT m_name FROM Movies WHERE release_year = 2023;
SELECT a_name FROM Actor WHERE charges = (SELECT MAX(charges) FROM Actor);
-- Replace <CITY1> and <CITY2> with the two cities required by your instructor.
SELECT a_name FROM Actor WHERE a_address NOT IN ('<CITY1>','<CITY2>');
SELECT m_name FROM Movies WHERE budget BETWEEN 10000000 AND 50000000;
```

## Notes / assumptions
The movie–actor relationship is many-to-many, so the junction table `Movie_Actor` is used. The workbook says “1cr to 5cr”; the sample query treats 1 crore as 10,000,000 and 5 crore as 50,000,000 in the chosen numeric currency representation.
