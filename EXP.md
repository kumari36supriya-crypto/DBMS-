### EXP.sql Documentation

This file documents the SQL statements in `EXP.sql`, describing the schema, sample data, and query sets (EXP1–EXP5).

---

### 1. Database and Schema Setup (Setup Only – No Questions)

- **Create the database**

  ```sql
  CREATE DATABASE 2cse21_0604;
  ```

- **Select the database**

  ```sql
  USE 2cse20_0396;
  ```

- **Create table `DEPARTMENT`**

  ```sql
  CREATE TABLE DEPARTMENT (
      DEPTNO INT PRIMARY KEY,
      DNAME VARCHAR(15) NOT NULL
  );
  ```

- **Create table `EMPLOYEE`**

  ```sql
  CREATE TABLE EMPLOYEE (
      EMPNO INT PRIMARY KEY,
      ENAME VARCHAR(20) NOT NULL,
      JOB VARCHAR(20),
      MGR INT,
      HIREDATE DATE,
      SAL DECIMAL(10,2),
      COMM DECIMAL(7,2),
      DEPTNO INT,
      FOREIGN KEY (DEPTNO) REFERENCES DEPARTMENT(DEPTNO)
  );
  ```

- **Insert records into `DEPARTMENT`**

  ```sql
  INSERT INTO DEPARTMENT VALUES
  (10,'RESEARCH'),
  (20,'ACCOUNTING'),
  (30,'SALES'),
  (40,'OPERATIONS');
  ```

- **Insert records into `EMPLOYEE`**

  ```sql
  INSERT INTO EMPLOYEE VALUES
  (7369,'SMITH','CLERK',7902,'1980-12-17',800,NULL,20),
  (7499,'ALLEN','SALESMAN',7698,'1981-02-20',1600,300,30),
  (7521,'WARD','SALESMAN',7698,'1981-02-22',1250,300,30),
  (7566,'JONES','MANAGER',7839,'1981-04-02',2975,NULL,20),
  (7654,'MARTIN','SALESMAN',7698,'1981-09-28',1250,1400,30),
  (7698,'BLAKE','MANAGER',7839,'1981-05-01',2850,NULL,30),
  (7782,'CLARK','MANAGER',7839,'1981-06-09',2450,NULL,20),
  (7788,'SCOTT','ANALYST',7566,'1982-12-09',3000,NULL,40),
  (7839,'KING','PRESIDENT',NULL,'1981-11-17',5000,NULL,20),
  (7844,'TURNER','SALESMAN',7698,'1981-09-08',1500,0,30),
  (7876,'ADAMS','CLERK',7788,'1983-01-12',1100,NULL,20),
  (7900,'JAMES','CLERK',7698,'1981-12-03',950,NULL,30),
  (7902,'FORD','ANALYST',7566,'1981-12-03',3000,NULL,20),
  (7934,'MILLER','CLERK',7782,'1982-01-23',1300,NULL,10);
  ```

- **Display all departments**

  ```sql
  SELECT * FROM DEPARTMENT;
  ```

- **Display all employeess**

  ```sql
  SELECT * FROM EMPLOYEE;
  ```

---

### 2. EXP1 – Basic DDL, DML, and Simple Queries

- **Q1. Create `Employee_master` from `EMPLOYEE`**

  ```sql
  CREATE TABLE Employee_master AS
  SELECT * FROM EMPLOYEE;
  ```

- **Q2. Display all records from `Employee_master`**

  ```sql
  SELECT * FROM Employee_master;
  ```

- **Q3. Delete all employees of department 10 from `Employee_master`**

  ```sql
  DELETE FROM Employee_master
  WHERE DEPTNO = 10;
  ```

- **Q4. Display `Employee_master` after deletion**

  ```sql
  SELECT * FROM Employee_master;
  ```

- **Q5. Increase salary by 10% for department 20 in `Employee_master`**

  ```sql
  UPDATE Employee_master
  SET SAL = SAL + (SAL * 0.10)
  WHERE DEPTNO = 20;
  ```

- **Q6. Display EMPNO, ENAME, SAL, DEPTNO for department 20 from `Employee_master`**

  ```sql
  SELECT EMPNO, ENAME, SAL, DEPTNO
  FROM Employee_master
  WHERE DEPTNO = 20;
  ```

- **Q7. Modify data type of `SAL` column in `Employee_master`**

  ```sql
  ALTER TABLE Employee_master
  MODIFY SAL DECIMAL(10,2);
  ```

- **Q8. Display all records from `Employee_master` after modification**

  ```sql
  SELECT * FROM Employee_master;
  ```

- **Q9. Drop the table `Employee_master`**

  ```sql
  DROP TABLE Employee_master;
  ```

---

### 3. EXP2 – Basic `SELECT` with Conditions

- **Q1. List distinct jobs from `EMPLOYEE`**

  ```sql
  SELECT DISTINCT JOB
  FROM EMPLOYEE;
  ```

- **Q2. List employees in department 30**

  ```sql
  SELECT *
  FROM EMPLOYEE
  WHERE DEPTNO = 30;
  ```

- **Q3. List distinct department numbers greater than 20**

  ```sql
  SELECT DISTINCT DEPTNO
  FROM EMPLOYEE
  WHERE DEPTNO > 20;
  ```

- **Q4. List employees in department 30 who are MANAGER or CLERK**

  ```sql
  SELECT *
  FROM EMPLOYEE
  WHERE DEPTNO = 30
  AND JOB IN ('MANAGER', 'CLERK');
  ```

- **Q5. List all clerks with EMPNO and DEPTNO**

  ```sql
  SELECT ENAME, EMPNO, DEPTNO
  FROM EMPLOYEE
  WHERE JOB = 'CLERK';
  ```

- **Q6. List managers not in department 30**

  ```sql
  SELECT *
  FROM EMPLOYEE
  WHERE JOB = 'MANAGER'
  AND DEPTNO <> 30;
  ```

- **Q7. List employees in department 10 whose job is not MANAGER or CLERK**

  ```sql
  SELECT *
  FROM EMPLOYEE
  WHERE DEPTNO = 10
  AND JOB NOT IN ('MANAGER', 'CLERK');
  ```

- **Q8. List employees whose salary is between 1200 and 1400**

  ```sql
  SELECT ENAME, JOB
  FROM EMPLOYEE
  WHERE SAL BETWEEN 1200 AND 1400;
  ```

- **Q9. List employees whose job is CLERK, ANALYST or SALESMAN**

  ```sql
  SELECT ENAME, DEPTNO
  FROM EMPLOYEE
  WHERE JOB IN ('CLERK', 'ANALYST', 'SALESMAN');
  ```

- **Q10. List employees whose name starts with 'M'**

  ```sql
  SELECT ENAME, DEPTNO
  FROM EMPLOYEE
  WHERE ENAME LIKE 'M%';
  ```

---

### 4. EXP3 – Ordering, Advanced `LIKE`, and Logical Operators

- **Q1. List employees of department 30 ordered by salary (descending)**

  ```sql
  SELECT ENAME, JOB, SAL
  FROM EMPLOYEE
  WHERE DEPTNO = 30
  ORDER BY SAL DESC;
  ```

- **Q2. List employees whose name starts with 'A', matches the pattern, and ends with 'N'**

  ```sql
  SELECT ENAME, JOB, DEPTNO
  FROM EMPLOYEE
  WHERE ENAME LIKE 'A%____%N';
  ```

- **Q3. List employees whose name starts with 'S'**

  ```sql
  SELECT *
  FROM EMPLOYEE
  WHERE ENAME LIKE 'S%';
  ```

- **Q4. List employees whose name contains 'S'**

  ```sql
  SELECT *
  FROM EMPLOYEE
  WHERE ENAME LIKE '%S%';
  ```

- **Q5. List employees whose name ends with 'S'**

  ```sql
  SELECT *
  FROM EMPLOYEE
  WHERE ENAME LIKE '%S';
  ```

- **Q6. List employees who are in department 10, 20, or 30 OR whose job is CLERK, SALESMAN, or ANALYST**

  ```sql
  SELECT ENAME, JOB, DEPTNO
  FROM EMPLOYEE
  WHERE DEPTNO IN (10,20,30)
  OR JOB IN ('CLERK', 'SALESMAN', 'ANALYST');
  ```

- **Q7. List employees having non-null commission**

  ```sql
  SELECT ENAME
  FROM EMPLOYEE
  WHERE COMM IS NOT NULL;
  ```

- **Q8. Find total salary (salary + commission) for each employee**

  ```sql
  SELECT EMPNO,
         SUM(SAL + IFNULL(COMM, 0)) AS TOTAL_SALARY
  FROM EMPLOYEE
  GROUP BY EMPNO;
  ```

- **Q9. Display department number and annual salary (SAL*12) for each employee**

  ```sql
  SELECT DEPTNO, SAL * 12 AS ANNUAL_SALARY
  FROM EMPLOYEE
  GROUP BY EMPNO;
  ```

- **Q10. List clerks whose salary is greater than 3000**

  ```sql
  SELECT ENAME
  FROM EMPLOYEE
  WHERE JOB IN ('CLERK') AND SAL > 3000;
  ```

- **Q11. List employees whose job is CLERK, SALESMAN, or ANALYST and salary is greater than 3000**

  ```sql
  SELECT ENAME
  FROM EMPLOYEE
  WHERE JOB IN ('CLERK', 'SALESMAN', 'ANALYST') AND SAL > 3000;
  ```

---

### 5. EXP4 – Date Conditions, String Functions, and Derived Columns

- **Q1. List employees hired before 30-06-1980 or after 31-12-1981**

  ```sql
  SELECT * FROM EMPLOYEE
  WHERE HIREDATE < '1980-06-30' OR HIREDATE > '1981-12-31';
  ```

- **Q2. List employees whose second letter of name is 'A'**

  ```sql
  SELECT ENAME FROM EMPLOYEE
  WHERE ENAME LIKE '_A%';
  ```

- **Q3. List employees whose name length is 5 characters**

  ```sql
  SELECT ENAME FROM EMPLOYEE
  WHERE LENGTH(ENAME) = 5;
  ```

- **Q4. List employees whose job is not CLERK, SALESMAN, or ANALYST**

  ```sql
  SELECT * FROM EMPLOYEE
  WHERE JOB NOT IN ('CLERK', 'SALESMAN', 'ANALYST');
  ```

- **Q5. Display EMPNO, ENAME and annual salary (SAL*12) ordered by salary descending**

  ```sql
  SELECT EMPNO, ENAME,
         SAL * 12 AS ANNUAL_SALARY
  FROM EMPLOYEE
  ORDER BY SAL DESC;
  ```

- **Q6. Display salary components (HRA, PF, DA) and total salary**

  ```sql
  SELECT ENAME, SAL,
         (SAL * 0.15) AS hra,
         (SAL * 0.05) AS pf,
         (SAL * 0.10) AS da,
         ((SAL + (SAL * 0.15) + (SAL * 0.10)) - (SAL * 0.05)) AS TOTALSALARY
  FROM EMPLOYEE
  ORDER BY TOTALSALARY DESC;
  ```

- **Q7. Update salary to 10% of its value where commission is NULL**

  ```sql
  UPDATE EMPLOYEE
  SET SAL = 0.1 * SAL
  WHERE COMM IS NULL;
  ```

- **Q8. List employees whose 120% of salary is greater than 3000**

  ```sql
  SELECT * FROM EMPLOYEE
  WHERE SAL * 1.2 > 3000;
  ```

- **Q9. List employees where length of salary value is at least 3 digits**

  ```sql
  SELECT * FROM EMPLOYEE
  WHERE LENGTH(SAL) >= 3;
  ```

---

### 6. EXP5 – Aggregate and String Functions

- **Q1. Count total number of employees**

  ```sql
  SELECT COUNT(*) FROM EMPLOYEE;
  ```

- **Q2. Display sum of salaries of all employees**

  ```sql
  SELECT SUM(SAL) FROM EMPLOYEE;
  ```

- **Q3. Display maximum salary**

  ```sql
  SELECT MAX(SAL) FROM EMPLOYEE;
  ```

- **Q4. Display minimum salary**

  ```sql
  SELECT MIN(SAL) FROM EMPLOYEE;
  ```

- **Q5. Display average salary**

  ```sql
  SELECT AVG(SAL) FROM EMPLOYEE;
  ```

- **Q6. Display maximum salary among clerks**

  ```sql
  SELECT MAX(SAL) FROM EMPLOYEE
  WHERE JOB = 'CLERK';
  ```

- **Q7. Display maximum salary in department 20**

  ```sql
  SELECT MAX(SAL) FROM EMPLOYEE
  WHERE DEPTNO = 20;
  ```

- **Q8. Display minimum salary among salesmen**

  ```sql
  SELECT MIN(SAL) FROM EMPLOYEE
  WHERE JOB = 'SALESMAN';
  ```

- **Q9. Display average salary of managers**

  ```sql
  SELECT AVG(SAL) FROM EMPLOYEE
  WHERE JOB = 'MANAGER';
  ```

- **Q10. Display total salary of analysts in department 40**

  ```sql
  SELECT SUM(SAL) FROM EMPLOYEE
  WHERE JOB = 'ANALYST' AND DEPTNO = 40;
  ```

- **Q11. Display employee names in uppercase**

  ```sql
  SELECT UPPER(ENAME) AS EMPLOYEE_NAME
  FROM EMPLOYEE;
  ```

- **Q12. Display employee names in lowercase**

  ```sql
  SELECT LOWER(ENAME) AS EMPLOYEE_NAME
  FROM EMPLOYEE;
  ```

- **Q13. Display employee names in proper case (first letter capital, rest small)**

  ```sql
  SELECT CONCAT(UPPER(LEFT(ENAME, 1)), LOWER(SUBSTRING(ENAME, 2)))
  FROM EMPLOYEE;
  ```

- **Q14. Display length of the string 'PRIYANSHU KUMAR YADAV'**

  ```sql
  SELECT LENGTH('PRIYANSHU KUMAR YADAV');
  ```

- **Q15. Display length of each employee name along with EMPNO and ENAME**

  ```sql
  SELECT LENGTH(ENAME), EMPNO, ENAME
  FROM EMPLOYEE;
  ```

---

