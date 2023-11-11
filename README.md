# SQL-Oracle-DB - Quiz 1 + 2 +3

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
