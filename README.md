# SQL-Oracle-DB - Quiz 1 + 2 + 3 + 4 + 5 + Mid(1) + 6 + 7 + 9 + 10(last) + Presentation

 > **Quiz 1**

1. Create Universities (UID, UNAME, ADDRESS, COUNTRY )  and
   Student tables(SID, SNAME, ADDRESS, COUNTRY, UID)
   That has One to Many Relationship (Primary/Foreign Key). Mark several columns as not null..

2. Add the rows to both tables

3. Write the Update STATEMENTS that modifies the Address for specific University

4. Write Select Statement that selects university addresses in the specific country

5. Write Select Statement that selects number of universities in the specific country

 > **Quiz 1 - Solution**

```js

-- Quiz 1: Student: Karam Elgamal - 201829

-- Universities Table
CREATE TABLE Universities (
    "UID" int NOT NULL PRIMARY KEY,
    UNAME VARCHAR2(50) NOT NULL,
    ADDRESS VARCHAR2(100) NOT NULL,
    COUNTRY VARCHAR2(50) NOT NULL
);

-- Students Table
CREATE TABLE Students (
    "SID" int NOT NULL PRIMARY KEY,
    SNAME VARCHAR2(50) NOT NULL,
    ADDRESS VARCHAR2(100) NOT NULL,
    COUNTRY VARCHAR2(50) NOT NULL,
    "UID" int,
    CONSTRAINT FK_University FOREIGN KEY ("UID") REFERENCES Universities("UID")
);

-- Insert into Universities Table

INSERT INTO Universities ("UID", UNAME, ADDRESS, COUNTRY)
VALUES (1, 'UG', '54 Main St', 'Georgia');

INSERT INTO Universities ("UID", UNAME, ADDRESS, COUNTRY)
VALUES (2, 'TSU', '12 Main St', 'Georgia');

-- Insert Data into Students Table

INSERT INTO Students ("SID", SNAME, ADDRESS, COUNTRY, "UID")
VALUES (1, 'Karam', 'Green Diamond', 'Georgia', 1);

INSERT INTO Students ("SID", SNAME, ADDRESS, COUNTRY, "UID")
VALUES (2, 'Ahmad', 'Marjan', 'Georgia', 1);


INSERT INTO Students ("SID", SNAME, ADDRESS, COUNTRY, "UID")
VALUES (3, 'Rami', 'Didi dghomi', 'Georgia', 2);

INSERT INTO Students ("SID", SNAME, ADDRESS, COUNTRY, "UID")
VALUES (4, 'hmode', 'ghomi', 'Georgia', 2);

-- Update STATEMENTS

UPDATE Universities
SET ADDRESS = '201 Rav St'
WHERE UNAME = 'UG';

-- Select STATEMENTS

SELECT UNAME, ADDRESS
FROM Universities
WHERE COUNTRY = 'Georgia';

SELECT COUNT(*)
FROM Universities
WHERE COUNTRY = 'Georgia';

```

 > **Quiz 2**

Tasks: 
1. Define the following tables:
- Countries: (Country_ID, Country_Name, Country_Population)
- Universities: (UniversityID, Uname, Country_ID)
- Students: (Sid, Sname,  S_age,UniversityID)
- Exams: (Sid, score, Subject)
- Grades: (Grade,  Min_Score ,  Max_Score )

2. Add the rows to these tables;

3. Write the join statements and ji0in the following tables together:
- Countries, universities, students
- Students, exams and grades

 > **Quiz 2 - Solution**

```js
-- Quiz 2: Student: Karam Elgamal - 201829

-- Create the Countries table
CREATE TABLE Countries (
    Country_ID INT PRIMARY KEY,
    Country_Name VARCHAR(255),
    Country_Population INT);

-- Create the Universities table
CREATE TABLE Universities (
    UniversityID INT PRIMARY KEY,
    Uname VARCHAR(255),
    Country_ID INT,
    FOREIGN KEY (Country_ID) REFERENCES Countries(Country_ID));

-- Create the Students table
CREATE TABLE Students (
    Sid INT PRIMARY KEY,
    Sname VARCHAR(255),
    S_age INT,
    UniversityID INT,
    FOREIGN KEY (UniversityID) REFERENCES Universities(UniversityID));

-- Create the Exams table
CREATE TABLE Exams (
    Sid INT,
    score INT,
    Subject VARCHAR(255),
    FOREIGN KEY (Sid) REFERENCES Students(Sid));

-- Create the Grades table
CREATE TABLE Grades (
    Grade VARCHAR(2) PRIMARY KEY,
    Min_Score INT,
    Max_Score INT);

-- Add rows to the Countries table
INSERT INTO Countries (Country_ID, Country_Name, Country_Population) VALUES (1, 'USA', 331002651);
INSERT INTO Countries (Country_ID, Country_Name, Country_Population) VALUES (2, 'Georgia', 1380004385);
INSERT INTO Countries (Country_ID, Country_Name, Country_Population) VALUES (3, 'Turkey', 1444216107);


-- Add rows to the Universities table
INSERT INTO Universities (UniversityID, Uname, Country_ID) VALUES (1, 'Harvard University', 1);
INSERT INTO Universities (UniversityID, Uname, Country_ID) VALUES (2, 'Stanford University', 1);
INSERT INTO Universities (UniversityID, Uname, Country_ID) VALUES (3, 'University of Georgia', 2);
INSERT INTO Universities (UniversityID, Uname, Country_ID) VALUES (4, 'New vision University', 2);
INSERT INTO Universities (UniversityID, Uname, Country_ID) VALUES (5, 'Peking University', 3);

-- Add rows to the Students table
INSERT INTO Students (Sid, Sname, S_age, UniversityID) VALUES (1, 'Karam Elgamal', 20, 3);
INSERT INTO Students (Sid, Sname, S_age, UniversityID) VALUES (2, 'Ahmad mohsn', 18, 3);
INSERT INTO Students (Sid, Sname, S_age, UniversityID) VALUES (3, 'David rafel', 21, 2);
INSERT INTO Students (Sid, Sname, S_age, UniversityID) VALUES (4, 'mayar jobran', 23, 4);
INSERT INTO Students (Sid, Sname, S_age, UniversityID) VALUES (5, 'hala mare', 23, 5);

-- Add rows to the Exams table
INSERT INTO Exams (Sid, score, Subject) VALUES (1, 90, 'Math');
INSERT INTO Exams (Sid, score, Subject) VALUES (1, 85, 'Science');
INSERT INTO Exams (Sid, score, Subject) VALUES (2, 92, 'Math');
INSERT INTO Exams (Sid, score, Subject) VALUES (3, 78, 'Math');
INSERT INTO Exams (Sid, score, Subject) VALUES (4, 87, 'Science');
INSERT INTO Exams (Sid, score, Subject) VALUES (5, 57, 'Science');

-- Add rows to the Grades table
INSERT INTO Grades (Grade, Min_Score, Max_Score) VALUES ('A', 90, 100);
INSERT INTO Grades (Grade, Min_Score, Max_Score) VALUES ('B', 80, 89);
INSERT INTO Grades (Grade, Min_Score, Max_Score) VALUES ('C', 70, 79);
INSERT INTO Grades (Grade, Min_Score, Max_Score) VALUES ('D', 51, 69);
INSERT INTO Grades (Grade, Min_Score, Max_Score) VALUES ('F', 0, 50);

-- Join Countries, Universities, and Students

-- 1)
SELECT * FROM Countries c inner JOIN Universities u ON c.Country_ID = u.Country_ID;
-- With {Using} clause
SELECT * FROM Students JOIN Universities USING (UniversityID); 


-- 2)
SELECT * FROM Countries c JOIN Universities u ON c.Country_ID = u.Country_ID JOIN Students s ON u.UniversityID = s.UniversityID;
-- With {Using} clause
SELECT * FROM Countries JOIN Universities USING(Country_ID) JOIN Students USING (UniversityID); 

-- Join Students, Exams, and Grades

-- 1)
SELECT * FROM Students s inner JOIN Exams e ON s.Sid = e.Sid; 


-- 2)
-- With {Using} clause
SELECT * FROM Students JOIN Exams e USING(Sid) JOIN Grades g ON e.score BETWEEN g.Min_Score AND g.Max_Score;
```
 > **Quiz 3**

Tasks: 
1. write inner join statement of scott.emp and scott.dept tables;
2. After joining of scott.emp and scott.dept tables display values of department name, employee name,job and salary columns;
3. Filter the rows that is returned in Task 2  and show only those rows that correspond to employees in sales department.
4. Write  left join statement of scott.emp nd scott.dept tbles;
5. Write natural join statement of scott.emp nd scott.dept tbles;
6. In the scott. emp table there is the column mgr that coresponds to the employee manager. Write the self join that  
   selects the employees data and their managers names

 > **Quiz 3 - Solution**
```js
-- Student: Karam Elgamal(201829)

-- Question 1
SELECT * FROM scott.emp INNER JOIN scott.dept USING(deptno);

-- Question 2
SELECT scott.dept.dname, scott.emp.ename, scott.emp.job, scott.emp.sal FROM scott.emp INNER JOIN scott.dept ON scott.emp.deptno = scott.dept.deptno;

-- Question 3
SELECT scott.dept.dname, scott.emp.ename, scott.emp.job, scott.emp.sal FROM scott.emp INNER JOIN scott.dept ON scott.emp.deptno = scott.dept.deptno WHERE scott.dept.dname = 'SALES';

-- Question 4
SELECT * FROM scott.emp e LEFT JOIN scott.dept d ON e.deptno = d.deptno;

-- Question 5
SELECT * FROM scott.emp NATURAL JOIN scott.dept;

-- Question 6
SELECT e.ename AS employee_name, e.job AS employee_job, m.ename AS manager_name, m.job AS manager_job FROM scott.emp e LEFT JOIN scott.emp m ON e.mgr = m.empno;

```

 > **Quiz 4**

Task 1. In an anonymous PL/SQL block, declare a function named - productNum which is passed two numeric variables as parameters and which calculates and returns the division of said two variables. In the execution section of the anonymous PL/SQL block, call the productNum function and display the value it returns.

Task 2. Modify the anonymous PL/SQL block created in  the task1 so that it should display 10 times the value returned after calling productNum function.

Task 3. In an anonymous PL/SQL block that was created in Task1 declare an additional numeric  variable and assign
the value to it returned by productNum function.

Task 4. Select the parameter values for the productNum function so that a division-by-zero exception occurs in its execution section. Refactor the productNum function so that it handles the exception. 

 > **Quiz 4 - Solution**
```js
-- Student: Karam Elgamal(201829)

-- Question 1
DECLARE number1 number; number2 number;
FUNCTION productNum (num1 IN number, num2 IN number) RETURN number IS res number;

BEGIN
  res := num1 / num2;
  RETURN res;
END;

BEGIN
  number1:= 20;
  number2:= 10;

  dbms_output.put_line('Product of (20,10): ' || productNum(number1, number2));
END;

-- Question 2

DECLARE number1 number; number2 number;
FUNCTION productNum (num1 IN number, num2 IN number) RETURN number IS res number;

BEGIN
  res := num1 / num2;
  RETURN res;
END;

BEGIN
  number1:= 20;
  number2:= 10;
  -- Print for 10 times
  FOR i IN 1..10 LOOP
    dbms_output.put_line(' Product of (20,10): ' || productNum(number1, number2));
  END LOOP;
END;

-- Question 3

DECLARE number1 number; number2 number; result number;
FUNCTION productNum (num1 IN number, num2 IN number) RETURN number IS res number;

BEGIN
  res := num1 / num2;
  RETURN res;
END;

BEGIN
  number1:= 20;
  number2:= 10;
  result:= productNum(number1, number2);

  dbms_output.put_line('Product of (20,10): ' || result);
END;

-- Question 4
 
DECLARE number1 number; number2 number;
FUNCTION productNum (num1 IN number, num2 IN number) RETURN number IS res number;

BEGIN
  res := num1 / num2;
  RETURN res;
END;

BEGIN
  number1:= 20;

  number2:= 0;

  dbms_output.put_line(' Product of (20,10): ' || productNum(number1, number2));
  EXCEPTION
    WHEN ZERO_DIVIDE THEN
    dbms_output.put_line('Error: Division by zero');
END;
```
 > **Quiz 5**

Task 1. In the following string: 'This is a general playlist ant this one is my playlist' start the search at the 5th character and find the index where the substring 'is' occurs the third time.

Task 2. Write a recursive function that takes an integer n as a parameter and calculates the factorial of n.

Task 3. Give an example of the to_timestamp() function that is given the string '25-Aug-2030 18:10:35.123456789' and the corresponding mask. The function should return a timestamp value.

Task 4. Write a select command that extracts records from the Scott.dept table and combines the values of the DNAM and LOC fields into a single field during the extraction process. The combined fields should look like this: DNAME-LOC

 > **Quiz 5 - Solution**
```js
-- Student: Karam Elgamal-201829

Declare
text1 VARCHAR(150) := 'This is a general playlist ant this one is my playlist';
date1 VARCHAR(150) := '25-Aug-2030 18:10:35.123456789';

BEGIN
    --Q1
   dbms_output.put_line('Start [' || INSTR(text1,'is',5, 3)|| ']');
   --Q3
	dbms_output.put_line(TO_TIMESTAMP(date1, 'DD-Mon-YYYY HH24:MI:SS.FF'));
END;

--Q2
CREATE OR REPLACE FUNCTION Factorial( n NUMBER ) RETURN NUMBER  IS
  BEGIN
    IF n <= 1 THEN 
      RETURN 1;
    ELSE
     RETURN n*Factorial(n-1);
   END IF;
  END Factorial;

SELECT Factorial(6) from dual;

--Q4
SELECT CONCAT(DNAME || ' ', LOC) AS Combined FROM Scott.dept;

```

 > **Midterm 1**
```js
-- Student: Karam Elgamal(201829)

-- Task 1:

CREATE TABLE Teams (
TeamID INT PRIMARY KEY,
TeamName VARCHAR(50) NOT NULL,
City VARCHAR(50) NOT NULL,
Country VARCHAR(50) NOT NULL
);

CREATE TABLE Players (
PlayerID INT PRIMARY KEY,
TeamID INT,
PlayerName VARCHAR(50) NOT NULL,
Age INT,
GoalsScored INT,
FOREIGN KEY (TeamID) REFERENCES Teams(TeamID)
);

CREATE TABLE PlayedGames (
MatchID INT PRIMARY KEY,
TeamA INT,
TeamB INT,
MatchResult VARCHAR(10) NOT NULL,
FOREIGN KEY (TeamA) REFERENCES Teams(TeamID),
FOREIGN KEY (TeamB) REFERENCES Teams(TeamID)
);

-- Task 2:

INSERT INTO Teams (TeamID, TeamName, City, Country)  VALUES 
(1, 'DinamoT', 'Tbilisi', 'Georgia');
INSERT INTO Teams (TeamID, TeamName, City, Country)  VALUES 
(2, 'DinamoB', 'Batumi', 'Georgia');
INSERT INTO Teams (TeamID, TeamName, City, Country)  VALUES 
(3, 'DinamoG', 'Gadauri', 'Georgia');
INSERT INTO Teams (TeamID, TeamName, City, Country)  VALUES 
(4, 'DinamoR', 'Rachpori', 'Israel');
INSERT INTO Teams (TeamID, TeamName, City, Country)  VALUES 
(5, 'DinamoM', 'Moscow', 'Russia');


INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(1, 1, 'Karam Elgamal', 21, 2);
INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(2, 1, 'Cristiano Ronaldo', 26, 2);
INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(3, 1, 'Lionel Messi', 35, 4);
INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(4, 1, 'Hakeem Ziech', 30, 0);

INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(5, 2, 'Gianluigi Buffon', 22, 0);
INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(6, 2, 'Luis Suarez', 34, 2);
INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(7, 2, 'Sergio Ramos', 39, 0);
INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(8, 2, 'Vincent Kompany', 38, 0);

INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(9,  3, 'Xavi', 40, 0);
INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(10, 3, 'Andres Iniesta', 20, 2);
INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(11, 3, 'Zlatan Ibrahimovic', 39, 0);
INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(12, 3, 'Radamel Falcao', 30, 2);

INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(13, 4, 'Robin van Persie', 19, 0);
INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(14, 4, 'Andrea Pirlo', 24, 0);
INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(15, 4, 'Yaya Toure', 32, 0);
INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(16, 4, 'Edinson Cavani', 26, 0);
INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(17, 5, 'Sergio Aguero', 18, 0);
INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(18, 5, 'Iker Casillas', 36, 2);
INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(19, 5, 'Neymar', 30, 0);
INSERT INTO Players (PlayerID, TeamID, PlayerName, Age, GoalsScored) VALUES
(20, 5, 'Sergio Busquets', 22, 3);

INSERT INTO PlayedGames (MatchID, TeamA, TeamB, MatchResult) VALUES
(1, 1, 2, 'DinamoT Won!');
INSERT INTO PlayedGames (MatchID, TeamA, TeamB, MatchResult) VALUES
(2, 3, 4, 'DinamoG Won!');
INSERT INTO PlayedGames (MatchID, TeamA, TeamB, MatchResult) VALUES
(3, 5, 1, 'DinamoM Won!');

-- Task 3:

-- 3.1:
SELECT Teams.Country, Players.PlayerName, Players.Age FROM Teams JOIN Players USING(TeamID);

-- 3.2:
SELECT Teams.Country, Players.PlayerName, Players.Age FROM Teams JOIN Players USING(TeamID) WHERE 
Teams.Country = 'Georgia' AND Players.Age > 22;

-- 3.4
SELECT Teams.Country, Players.PlayerName, Players.Age FROM (
SELECT Teams.Country, Players.PlayerName, Players.Age FROM Teams JOIN Players USING(TeamID) WHERE Teams.Country = 'Georgia' AND Players.Age > 25
) AS ResultTable WHERE AverageAge > 25;

-- 3.6
SELECT
    T1.TeamName AS TeamA,
    P1.PlayerName AS PlayerA,
    T2.TeamName AS TeamB,
    P2.PlayerName AS PlayerB
FROM
    Teams T1
JOIN
    Players P1 ON T1.TeamID = P1.TeamID
JOIN
    Teams T2 ON T1.TeamID < T2.TeamID -- Ensures no duplicate combinations
JOIN
    Players P2 ON T2.TeamID = P2.TeamID
LEFT JOIN
    PlayedGames PG ON (T1.TeamID = PG.TeamA AND T2.TeamID = PG.TeamB) OR (T1.TeamID = PG.TeamB AND T2.TeamID = PG.TeamA)
WHERE
    PG.MatchID IS NULL;


-- Task 4:
CREATE OR REPLACE FUNCTION SUMFunction (n IN number) RETURN number IS res number:=0;
BEGIN
FOR i IN 1..n LOOP
res := res + i;
END LOOP;
RETURN res;
END;
BEGIN
  dbms_output.put_line('SUM:' || SUMFunction(5));
END;

```
 > **Quiz 6**

Task 1. Select average, max, min and total salaries in single select statement

Task 2. Group select average, max, min and total salaries by department number

Task 3. Filter the rows in the task 2 based the condition average salary is greater than 9000

 > **Quiz 6 - Solution**
```js
-- Student: Karam Elgamal(201829)

-- Q1
SELECT 
    AVG(sal),
    MAX(sal),
    MIN(sal),
    SUM(sal)
FROM scott.emp;

-- Q2
SELECT 
    AVG(sal),
    MAX(sal),
    MIN(sal),
    SUM(sal)
FROM scott.emp GROUP BY DEPTNO;

-- Q3
SELECT 
    AVG(sal),
    MAX(sal),
    MIN(sal),
    SUM(sal)
FROM scott.emp GROUP BY DEPTNO having AVG(sal)>9000;
```

 > **Quiz 7**

Task 1. What is a subquery, and how is it different from a regular query?

Task 2. Write a subquery to find the names of employees (from scott.emp) who work in the department with
the highest average salary.

Task 3. Explain the difference between a correlated subquery and a non-correlated subquery.

Task 4. Use a subquery to find the department names (from scott.dept) that have at least one employee (from
scott.emp).

Task 5. Write a subquery to find the employees (from scott.emp) who earn more than the average salary in
their respective departments (from scott.dept).

 > **Quiz 7 - Solution**
```js
-- Student: Karam Elgamal(201829)

-- Q1
-- A sub query, as its name implies, is a query that is nested inside a main query and is typically used as a need to retrieve particular data from a table.
-- As mentioned above, it differs from a regular query in that it is nested within another query and serves the primary query's purpose of obtaining data from a table.

-- Q2
SELECT ename FROM scott.emp WHERE deptno = 
(
    SELECT deptno FROM scott.emp GROUP BY deptno
    ORDER BY AVG(sal) DESC FETCH FIRST 1 ROW ONLY
);

-- Q3
-- Both are types of sub-queries, the diffrence is that in a noncorrelated subquery obtains its results independently of its main statement. 
-- While the correlated subquery requires values from its main query in order to execute.

-- Q4
SELECT d.dname FROM scott.dept d WHERE d.deptno IN 
(
    SELECT e.deptno
    FROM scott.emp e
);

-- Q5
SELECT * FROM scott.emp e WHERE sal > 
(
    SELECT AVG(sal)
    FROM scott.emp
    WHERE deptno = e.deptno
);
```
> **Quiz 9**

Task 1. Write a SQL query to retrieve the names (ename) and salaries (sal) of employees from the emp table who earn more than the average salary of their respective departments.

Task 2.Create a SQL query that lists the department numbers (deptno) and the total number of employees in each department from the emp table. Use a subquery in your solution.

Task 3. Compose a SQL query to find the employee names (ename) and job titles (job) of those employees who have the same job title as the employee with the name 'SMITH'.

Task 4.Write a SQL query to retrieve the department numbers (deptno) and the maximum salary (sal) in each department from the emp table. Utilize a subquery to achieve this.

 > **Quiz 9 - Solution**
```js
-- Student: Karam Elgamal(201829)

--Q1
SELECT ename, sal FROM scott.emp e1 WHERE sal > (
    SELECT AVG(sal) FROM scott.emp e2 WHERE e1.deptno = e2.deptno
    );

--Q2
SELECT deptno, 
       (SELECT COUNT(*) FROM Scott.emp e2 WHERE e2.deptno = e1.deptno) AS total_emp
FROM Scott.emp e1
GROUP BY deptno;

--Q3
SELECT ename, job
FROM Scott.emp
WHERE job = (SELECT job FROM Scott.emp WHERE ename = 'SMITH');

--Q4
SELECT deptno, 
       (Select MAX(sal) FROM Scott.emp e2 WHERE e2.deptno = e1.deptno) as Max_sal
FROM Scott.emp e1
GROUP BY deptno;
```
> **Quiz 10 - Last**

Task 1. Write the Inner join, left Outer Join, right outer join, cross join and natural join. Describe the difference between iner join and left outer join.

Task 2. Write several select statements on emp table that uses several aggregation functions to aggregate salary data by deptno column. Restrict output by filtering In the select statement, using the having clause, filter the values of the aggregation function.

Task 3. Write a select that returns the records of employees who earn more than the average salary in theirdepartment.

Task 4. Write a select that returns records of employees who have a salary greater than the average salary and less than the maximum salary in their department.

Task 5. Write the query statements that selects all columns from Emp table and one additional column – HireMonth. This additional column should contain information about the month of the year in which the employee was hired.

Task 6. Write the query statements that selects all columns from Emp table and one additional column – EnameAndJob. This additional column should contain string values obtained through the concatenation of Ename and Job columns: Ename -Job.

 > **Quiz 10 - Solution**
```js
-- Student: Karam Elgamal(201829)

-- Q1 (Joins)

-- Inner join
Select * from scott.dept d inner join scott.emp e on d.deptno = e.deptno;

-- Left join
Select * from scott.dept d left outer join scott.emp e on d.deptno = e.deptno;

-- Right join
Select * from scott.dept d right outer join scott.emp e on d.deptno = e.deptno;

-- Cross Join:
SELECT * FROM scott.emp CROSS JOIN scott.dept;

-- Natural Join:
Select * from scott.dept d Natural join scott.emp e;

-- INNER JOIN returns only the rows where there is a match in both tables based on the specified condition.
-- LEFT OUTER JOIN returns all rows from the left table (the one listed before the LEFT OUTER JOIN clause), and the matched rows from the right table.

-- Q2 (Aggregation function)

-- Aggregate salary
select sum(sal) from scott.emp;

-- Sum + Avg + max + min salary grouped by deptno;
select deptno, sum(sal), avg(sal), max(sal), min(sal) from scott.emp group by deptno;

-- Restrict output by filtering: Avg salary value between 3000 - 1000
select deptno, sum(sal), avg(sal), max(sal), min(sal) from scott.emp group by deptno having avg(sal)>1000 and avg(sal) < 3000;

-- Q3 
-- We join the scott.emp talbe with (deptno, avg(sal)) table and name it "dept_avg". We join it using the deptno and then apply the condition. {e. is used to select all the emps fields from the table we joined, if we use * it selects all cloums of the joined table}
SELECT e.*
FROM scott.emp e
JOIN (
    SELECT deptno, AVG(sal) AS avg_salary
    FROM scott.emp
    GROUP BY deptno
) dept_avg ON e.deptno = dept_avg.deptno
WHERE e.sal > dept_avg.avg_salary;

-- Q4
SELECT e.*
FROM scott.emp e
JOIN (
    SELECT deptno, avg(sal) AS avg_salary, max(sal) as max_salary
    FROM scott.emp
    GROUP BY deptno
) dept_stats ON e.deptno = dept_stats.deptno
WHERE e.sal > dept_stats.avg_salary and e.sal<dept_stats.max_salary ;

-- Q5
select e.*, to_char(HIREDATE,'MM') as Hire_Year from scott.emp e;
select e.*, extract(month from HIREDATE) as Hire_Year from scott.emp e;

-- Q6
select e.*, ename||'-'||job as NameAndJob from scott.emp e;
```
> **Presentation**

Task: Create a database and related tables for retail banking. Tables should be created to store information about the following objects:
1. Clients
2. Client accounts and balances on them/
3. Transfers from one account to another

Create a procedure that adds a new record to the transfers table. On the transfers table, create a trigger that will change the balances on the respective accounts when a new record appears in the transfers table

 > **Solution**
```js
-- Student: Karam Elgamal(201829)
-- Presentation

-- Clients table
CREATE TABLE Clients (
    client_id INT PRIMARY KEY,
    Name VARCHAR(255),
    phone VARCHAR(20),
    country VARCHAR(255)
);

-- ClientAccounts table
CREATE TABLE ClientAccounts (
    account_id INT PRIMARY KEY,
    client_id INT,
    balance DECIMAL(10, 2),
    FOREIGN KEY (client_id) REFERENCES Clients(client_id)
);


-- Transfers table
CREATE TABLE Transfers (
    transfer_id INT PRIMARY KEY,
    sender_id INT,
    receiver_id INT,
    amount DECIMAL(10, 2),
    transfer_date TIMESTAMP,
    FOREIGN KEY (sender_id) REFERENCES ClientAccounts(account_id),
    FOREIGN KEY (receiver_id) REFERENCES ClientAccounts(account_id)
);

-- Insert mock data
INSERT INTO Clients VALUES (1, 'Karam Elgamal', '0584040447', 'Georgia'); -- Has two accounts
INSERT INTO Clients VALUES (2, 'Malik wasel','0584234091', 'US');
INSERT INTO Clients VALUES (3, 'Waseem Haj','0506278202', 'Russia');
INSERT INTO ClientAccounts VALUES (100, 1, 5000.00);
INSERT INTO ClientAccounts VALUES (101, 2, 2500.00);
INSERT INTO ClientAccounts VALUES (102, 3, 7500.00);
INSERT INTO ClientAccounts VALUES (103, 1, 1500.00);

-- Sequence for transfer_id
CREATE SEQUENCE SeqTransfer_id START WITH 1 INCREMENT BY 1;

-- Procedure that adds a new record to the transfers table
CREATE OR REPLACE PROCEDURE AddTransfer(sender_id INT,receiver_id INT,amount DECIMAL) IS
BEGIN
    INSERT INTO Transfers(transfer_id, sender_id, receiver_id, amount, transfer_date)
    VALUES (SeqTransfer_id.NEXTVAL, sender_id, receiver_id, amount, SYSTIMESTAMP);
END;

-- Trigger to update balance of the sender and receiver
CREATE OR REPLACE TRIGGER UpdateBalances
AFTER INSERT ON Transfers
FOR EACH ROW
DECLARE
    sender_balance DECIMAL;
    receiver_balance DECIMAL;
BEGIN
    -- Get the current balances of both sender & receiver
    SELECT balance INTO sender_balance FROM ClientAccounts WHERE account_id = :NEW.sender_id;
    SELECT balance INTO receiver_balance FROM ClientAccounts WHERE account_id = :NEW.receiver_id;

    -- Update the balances accordingly
    UPDATE ClientAccounts SET balance = sender_balance - :NEW.amount WHERE account_id = :NEW.sender_id;
    UPDATE ClientAccounts SET balance = receiver_balance + :NEW.amount WHERE account_id = :NEW.receiver_id;
END;

-- Testing(AddTransfer procedure & Trigger balance change)
BEGIN
    AddTransfer(100, 101, 2500.00);
    AddTransfer(103, 102, 500.00);
END;

-- Testing select data
select * from Transfers;
select * from Clients;
select * from ClientAccounts;
```
