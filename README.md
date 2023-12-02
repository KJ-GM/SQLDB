# SQL-Oracle-DB - Quiz 1 + 2 + 3 + 4 + 5 + Mid(1)

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

Task 1. In the following string: 'This is a general playlist ant this one is my playlist' start the search at the 5th character and find the index where the substring 'is' occurs the third time.

Task 2. Write a recursive function that takes an integer n as a parameter and calculates the factorial of n.

Task 3. Give an example of the to_timestamp() function that is given the string '25-Aug-2030 18:10:35.123456789' and the corresponding mask. The function should return a timestamp value.

Task 4. Write a select command that extracts records from the Scott.dept table and combines the values of the DNAM and LOC fields into a single field during the extraction process. The combined fields should look like this: DNAME-LOC > **Quiz 5**
```js
test
```
