## ✅ PRACTICE 7 — SUBQUERIES

**1) Same department (exclude entered employee)**
```sql
SELECT last_name, hire_date
FROM employees
WHERE department_id = (
    SELECT department_id
    FROM employees
    WHERE last_name = '&name'
)
AND last_name <> '&name';
```

**2) Salary greater than average**
```sql
SELECT employee_id, last_name, salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
)
ORDER BY salary;
```

**3) Employees in dept with any 'u' in last name**
```sql
SELECT employee_id, last_name
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM employees
    WHERE last_name LIKE '%u%'
);
```

**4) Employees by location**

Fixed:
```sql
SELECT last_name, department_id, job_id
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE location_id = 1700
);
```

Prompt:
```sql
SELECT last_name, department_id, job_id
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE location_id = &location_id
);
```

**5) Employees reporting to King**
```sql
SELECT last_name, salary
FROM employees
WHERE manager_id = (
    SELECT employee_id
    FROM employees
    WHERE last_name = 'King'
);
```

**6) Executive department employees**
```sql
SELECT department_id, last_name, job_id
FROM employees
WHERE department_id = (
    SELECT department_id
    FROM departments
    WHERE department_name = 'Executive'
);
```

**7) Above average + department with 'u'**
```sql
SELECT employee_id, last_name, salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
)
AND department_id IN (
    SELECT department_id
    FROM employees
    WHERE last_name LIKE '%u%'
);
```

## ✅ PRACTICE 8 — SET OPERATORS

**1) Departments without ST_CLERK**
```sql
SELECT department_id
FROM departments
MINUS
SELECT department_id
FROM employees
WHERE job_id = 'ST_CLERK';
```

**2) Countries with no departments**
```sql
SELECT country_id, country_name
FROM countries
MINUS
SELECT c.country_id, c.country_name
FROM countries c
JOIN locations l ON c.country_id = l.country_id
JOIN departments d ON l.location_id = d.location_id;
```

**3) Jobs in dept 10, 50, 20 (order)**
```sql
SELECT job_id, department_id FROM employees WHERE department_id = 10
UNION ALL
SELECT job_id, department_id FROM employees WHERE department_id = 50
UNION ALL
SELECT job_id, department_id FROM employees WHERE department_id = 20;
```

**4) Same current job as original**
```sql
SELECT employee_id, job_id
FROM employees
INTERSECT
SELECT employee_id, job_id
FROM job_history;
```

**5) Employees + departments (even if missing)**
```sql
SELECT last_name, department_id, TO_CHAR(NULL) department_name
FROM employees
UNION
SELECT TO_CHAR(NULL), department_id, department_name
FROM departments;
```

## ✅ PRACTICE 9 — DML + TRANSACTIONS

**Create table**
```sql
CREATE TABLE my_employee (
 id NUMBER(4) NOT NULL,
 last_name VARCHAR2(25),
 first_name VARCHAR2(25),
 userid VARCHAR2(8),
 salary NUMBER(9,2)
);
```

**Insert**
```sql
INSERT INTO my_employee VALUES (1,'Patel','Ralph','rpatel',895);

INSERT INTO my_employee (id,last_name,first_name,userid,salary)
VALUES (2,'Dancs','Betty','bdancs',860);
```

**Script insert**
```sql
INSERT INTO my_employee (id,last_name,first_name,userid,salary)
VALUES (&id,'&last_name','&first_name','&userid',&salary);
```

**Update**
```sql
UPDATE my_employee
SET last_name='Drexler'
WHERE id=3;

UPDATE my_employee
SET salary=1000
WHERE salary < 900;
```

**Delete**
```sql
DELETE FROM my_employee
WHERE last_name='Dancs' AND first_name='Betty';
```

**Transactions**
```sql
COMMIT;

SAVEPOINT sp1;

DELETE FROM my_employee;

ROLLBACK TO sp1;
```

**Auto USERID script**
```sql
INSERT INTO my_employee (id,last_name,first_name,userid,salary)
VALUES (
 &id,
 '&last_name',
 '&first_name',
 LOWER(SUBSTR('&first_name',1,1)||SUBSTR('&last_name',1,7)),
 &salary
);
```

## ✅ PRACTICE 10 — DDL

**1) Create DEPT**
```sql
CREATE TABLE dept (
 id NUMBER(7) NOT NULL,
 name VARCHAR2(25)
);
```

**2) Insert from departments**
```sql
INSERT INTO dept (id,name)
SELECT department_id, department_name
FROM departments;
```

**3) Create EMP**
```sql
CREATE TABLE emp (
 id NUMBER(7),
 last_name VARCHAR2(25),
 first_name VARCHAR2(25),
 dept_id NUMBER(7)
);
```

**4) Create EMPLOYEES2**
```sql
CREATE TABLE employees2 AS
SELECT employee_id AS id,
       first_name,
       last_name,
       salary,
       department_id AS dept_id
FROM employees
WHERE 1=2;
```

**5) Read only**
```sql
ALTER TABLE employees2 READ ONLY;
```

**6–7) Insert after read/write**
```sql
ALTER TABLE employees2 READ WRITE;

INSERT INTO employees2
VALUES (34,'Grant','Marcie',5678,10);
```

**8) Drop table**
```sql
DROP TABLE employees2;
```

**9) Primary key**
```sql
ALTER TABLE emp
ADD CONSTRAINT my_emp_id_pk PRIMARY KEY(id);
```

**10) Foreign key**
```sql
ALTER TABLE emp
ADD CONSTRAINT my_emp_dept_id_fk
FOREIGN KEY (dept_id)
REFERENCES dept(id);
```

## 🚀 LAST MINUTE TIP (VERY IMPORTANT)

Memorize these patterns:

*   `salary > (SELECT AVG...)` ⭐
*   `department_id IN (SELECT...)` ⭐
*   `MINUS / UNION ALL` ⭐
*   `INSERT / UPDATE / DELETE` ⭐
*   `COMMIT / ROLLBACK / SAVEPOINT` ⭐
*   `CREATE TABLE AS SELECT` ⭐
*   `PRIMARY KEY / FOREIGN KEY` ⭐
