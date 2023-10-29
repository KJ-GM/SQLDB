# SQL-Oracle-DB

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
