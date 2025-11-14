						Sub-Languages
						--------------------
	Types of Sub-Languages
	--------------------------------
	1.DDL	(Data Defination Language)
	2.DML	(Data Manuplation Language)
	3.DRL	(Data Retrival Language)
	4.TCL	(Transaction Control Language)
	5.DCL	(Data Control Language)

	1.DDL	(Data Defination Language)
	--------------------------------------------------
	DDL Sub-Language is used to Create / Define the Databases , Database Objects like (Tables)
	It is also used to Change the Existing table Structure

	Create , Alter , Add , Drop , Truncate

	Create  --> It is used to Create / Define the Databases , Database Objects like (Tables)

	Alter  --> It is also used to Change the Existing table Structure

	Add  --> It is used to Add the Columns to an Existing Tables

	Drop  --> It is used to Remove the Columns from the Tables	( Drop the Tables , Databases)	***(No Rollback)

	Truncate  --> It is used to Remove the Complete Data in the Tables		***(No Rollback Data)

	2.DML	(Data Manuplation Language)
	-----------------------------------------------------
	DML Sub-Language is used to Insert , Update , Delete the Data in the Tables

	Insert , Update , Delete

	Insert  --> It is used to Insert the New Data into the Tables
	
	Update  --> It is used to Modify the Old Data in the Tables

	Delete  --> It is used to Remove the Unwanted Data in the Tables	***(Rollback Data)

	3.DRL	(Data Retrival Language)
	-----------------------------------------------
	DRL Sub-Language is used to Retrieve / Fetch / get the Data from the Tables

	Select  --> It is used to Retrieve / Fetch / get the Data from the Tables

	Where  --> It is used to Filter the Data in the Tables

	4.TCL	(Transaction Control Language)
	--------------------------------------------------------
	TCL Sub-Language is used to Control the DML Operations	(Insert , Update , Delete)

	Commit , Rollback , SavePoint

	Commit  --> It is used to Permentelly Stores the Data in the Tables

	Rollback  --> It is used to go back to the Previous Position of the Tables

	SavePoint  --> It is used to Commit / Rollback a Particular Transaction

	5.DCL	(Data Control Language)
	---------------------------------------------

	Grant  --> It is used to give the Access to the Users

	Revoke  --> It is used to Remove the Access to the User

-------------------------------------------------------------------------------------------------------------------------


					-- DDL SUB-LANGUAGE

CREATE DATABASE SUB_LANGUAGES

USE SUB_LANGUAGES

CREATE TABLE EMPLOYEES(ENO INT,ENAME VARCHAR(20),SALARY MONEY,DNO INT)

-- HOW TO SEE THE TABLE STRUCTURE
SP_HELP EMPLOYEES

					-- ALTER
-- how to change the Data type of the Columns
ALTER TABLE EMPLOYEES ALTER COLUMN ENO BIGINT

-- HOW TO CHANGE THE SIZE OF THE COLUMNS
ALTER TABLE EMPLOYEES ALTER COLUMN ENAME VARCHAR(50)

					-- ADD
-- HOW TO ADD THE COLUMNS TO AN EXSITING TABLES
ALTER TABLE EMPLOYEES ADD JOB VARCHAR(20)

					-- DROP
-- HOW TO REMOVE THE COLUMNS FROM AN EXISTING TABLE
ALTER TABLE EMPLOYEES DROP COLUMN JOB

DROP TABLE EMPLOYEES

CREATE DATABASE AB

DROP DATABASE AB

				-- TRUNCATE
TRUNCATE TABLE EMPLOYEES

------------------------------------------------------------------------------------------------------------------------------------------------

							-- DML SUB-LANGUAGE

CREATE TABLE EMP(ENO INT,ENAME VARCHAR(20),JOB VARCHAR(20),SALARY INT,DNO INT)

-- INSERT
INSERT INTO EMP VALUES(101,'WARNER','DEV',12000,10)
INSERT INTO EMP VALUES(102,'SMITH','SALES',14000,20)
INSERT INTO EMP VALUES(103,'SCOOT','ADMIN',16000,30)
INSERT INTO EMP VALUES(104,'FINCH','DEV',18000,10)
INSERT INTO EMP VALUES(105,'STARCH','SALES',20000,20)
INSERT INTO EMP VALUES(106,'MAXWELL','DEV',21000,10)

INSERT INTO EMP (ENO,ENAME,SALARY) VALUES(107,'ABD',22000)

SELECT * FROM EMP

-- UPDATE
UPDATE EMP SET SALARY=30000

UPDATE EMP SET SALARY=30000 WHERE ENO=101

UPDATE EMP SET SALARY=25000,DNO=20 WHERE ENO=103

UPDATE EMP SET JOB='ADMIN',SALARY=35000,DNO=30 WHERE ENO=105

-- DELETE
DELETE FROM EMP

DELETE FROM EMP WHERE ENO=105

					-- DRL SBU-LANGUAGE
-- SELECT

SELECT * FROM EMP

SELECT ENO,ENAME,SALARY FROM EMP

-- WHERE
SELECT ENO,ENAME,JOB,SALARY FROM EMP WHERE ENO=101

SELECT * FROM EMP WHERE DNO=10

		-- DIFFERENT WAYS TO SELECT THE DATA FROM THE TABLES

		SELECT * FROM EMP							-- ONE PART NAME
		SELECT * FROM DBO.EMP						-- TWO PART NAME
		SELECT * FROM SUB_LANGUAGES.DBO.EMP			-- THREE PART NAME

------------------------------------------------------------------------------------------------------------------------------------------------------


	How to Rename the Column Names
	How to Rename the Table Names
	How to Rename the Database Names

	How to Copy the Data from One Table to Another Table
	How to Copy the Data from One Database to Another Database

------------------------------------------------------------------------------------------------------------------------------------------------------


CREATE TABLE EMP(ENO INT,ENAME VARCHAR(20),SALARY INT,DNO INT)

INSERT INTO EMP VALUES(101,'WARNER',12000,10)
INSERT INTO EMP VALUES(102,'SMITH',14000,20)
INSERT INTO EMP VALUES(103,'SCOOT',16000,30)
INSERT INTO EMP VALUES(104,'FINCH',18000,10)

SELECT * FROM EMPLOYEES

-- HOW TO RENAME THE COLUMN NAMES
SP_RENAME 'EMP.ENO','EID'

-- HOW TO RENAME THE TABLE NAMES
SP_RENAME 'EMP','EMPLOYEES'

-- HOW TO RENAME THE DATABASE NAMES
CREATE DATABASE AB

SP_RENAMEDB 'AB','ANALYTICS BENCHMARK'

		-- HOW TO COPY THE DATA FROM ONE TABLE TO ANOTHER TABLE

/* RULES
1.THE NO.OF COLUMNS IN THE DESTINATION TABLE AND THE SELECT QUERY HAS TO BE SAME
2.POSITION OF THE COLUMNS IN THE DESTINATION TABLE AND THE SELECT QUERY HAS TO BE SAME
3.DATA TYPE OF THE COLUMNS IN THE DESTINATION TABLE AND THE SELECT QUERY HAS TO BE SAME
*/

CREATE TABLE EMP1(ENO INT,ENAME VARCHAR(20),SALARY INT,DNO INT)

INSERT INTO EMP1 VALUES(101,'WARNER',12000,10)
INSERT INTO EMP1 VALUES(102,'SMITH',14000,20)
INSERT INTO EMP1 VALUES(103,'SCOOT',16000,30)
INSERT INTO EMP1 VALUES(104,'FINCH',18000,10)

SELECT * FROM EMP1

CREATE TABLE EMP2(ENO INT,ENAME VARCHAR(20),SALARY INT,DNO INT)

SELECT * FROM EMP1
SELECT * FROM EMP2

INSERT INTO EMP2 SELECT * FROM EMP1

CREATE TABLE EMP3(ENO INT,ENAME VARCHAR(20))

SELECT * FROM EMP1
SELECT * FROM EMP3

INSERT INTO EMP3 SELECT ENO,ENAME FROM EMP1

-- HOW TO COPY NTHE DATA FROM SOURCE TO DESTINATION WITHOUT HAVING THE DESTINATION TABLE
SELECT * INTO EMP4 FROM EMP1

SELECT * FROM EMP4

-- HOW TO COPY THE DATA FROM ONE DATABASE TO ANOTHER DATABASE
CREATE DATABASE S1

CREATE TABLE EMP(ENO INT,ENAME VARCHAR(20),SALARY INT)

INSERT INTO EMP VALUES(101,'WARNER',12000)
INSERT INTO EMP VALUES(102,'SMITH',14000)
INSERT INTO EMP VALUES(103,'SCOOT',16000)
INSERT INTO EMP VALUES(104,'FINCH',18000)

SELECT * FROM EMP

CREATE DATABASE S2

CREATE TABLE EMP1(ENO INT,ENAME VARCHAR(20),SALARY INT)

SELECT * FROM EMP1

INSERT INTO S2.DBO.EMP1 SELECT * FROM S1.DBO.EMP

SELECT * INTO S2.DBO.EMP2 FROM S1.DBO.EMP

SELECT * FROM EMP2



























