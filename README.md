# Introduction to Databases (Using the HR Database)
What is a Database?

A database is an organized collection of related data that is stored electronically. It allows users to store, retrieve, update, and delete information efficiently.

In your HR Database, information about employees, attendance, payroll, and leave requests is stored in separate tables. Together, these tables form a single database called the HR Database.

Example

Your HR database contains tables such as:

- employees – Stores employee details.
- attendance – Stores employee attendance records.
- payroll – Stores salary information.
- leave_requests – Stores employee leave applications.

Instead of keeping this information in multiple Excel files, everything is organized inside one database.

# Why Do We Need a Database?

Imagine a company with 5,000 employees.

Without a database:

- Employee details are stored in Excel.
- Attendance is stored in another file.
- Payroll is stored in another file.
- Leave requests are stored separately.

Finding one employee's complete information becomes difficult.

With the HR Database:

- Employee information is connected using Employee IDs.
- Attendance, payroll, and leave records can be accessed instantly.
- Reports can be generated using SQL queries.

# What is a DBMS?

A Database Management System (DBMS) is software used to create and manage databases.

In your project, you use MySQL, which is a DBMS.

The DBMS allows you to:

- Create tables
- Insert employee records
- Update salaries
- Delete records
- Search information using SQL
- Maintain security and backups

Example:

SELECT * FROM employees;
The DBMS retrieves all employee records from the employees table.

<img width="1112" height="522" alt="image" src="https://github.com/user-attachments/assets/4ce4b0b8-8925-4a0d-8b65-921823358531" />

# What is an RDBMS?

An RDBMS (Relational Database Management System) stores data in related tables.

Your HR database is an example of an RDBMS because:

- Employee information is stored in one table.
- Attendance information is stored in another table.
- Payroll information is stored in another table.
- Leave information is stored in another table.

These tables are connected using employee_id.

  <img width="335" height="235" alt="image" src="https://github.com/user-attachments/assets/91489c17-2570-4266-8081-58ec62ea5902" />

# Benefits of Using the HR Database
- Employee information is stored only once.
- Attendance records are linked to employees.
- Payroll is calculated separately without duplicating employee details.
- Leave requests are tracked efficiently.
- SQL queries can combine data from multiple tables to generate reports.

Example:

SELECT  e.first_name, e.last_name, p.basic_pay FROM employees e JOIN payroll p ON e.employee_id = p.employee_id;

This query displays each employee's name along with their salary.

<img width="750" height="588" alt="image" src="https://github.com/user-attachments/assets/bba0accb-d635-471d-9e3b-aeb66386e908" />

Advantages of Your HR Database

- Reduced redundancy: Employee details are stored once.
- Data consistency: Updates are reflected across related records.
- Data integrity: Relationships between tables maintain valid references.
- Easy reporting: SQL joins enable comprehensive reports.
- Security: User access can be controlled by the DBMS.
- Scalability: New employees and records can be added without redesigning the database.
# SQL Commands

SQL (Structured Query Language) is the standard language used to communicate with relational databases. SQL commands are classified into five categories:

DDL (Data Definition Language)
DML (Data Manipulation Language)
DQL (Data Query Language)
DCL (Data Control Language)
TCL (Transaction Control Language)
# 1. DDL (Data Definition Language)

DDL commands are used to define and modify the structure of database objects such as tables.

1.CREATE

Creates a new table.
Example:
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    department VARCHAR(50),
    salary DECIMAL(10,2)
);

Output

<img width="932" height="410" alt="image" src="https://github.com/user-attachments/assets/9427f4ad-ab0e-45e8-a6ca-8df3c7f97624" />

2.ALTER

Modifies an existing table.
Example: Add an email column to the employees table.
ALTER TABLE employees ADD email VARCHAR(100);

<img width="1176" height="285" alt="image" src="https://github.com/user-attachments/assets/248b9fdb-78a8-4fef-b0e3-05e2d3e02967" />

3.DROP

Deletes an entire table.
Example
DROP TABLE attendance;
Result
<img width="1201" height="267" alt="image" src="https://github.com/user-attachments/assets/3917efd0-478e-4cd6-972b-05ba57f28583" />

TRUNCATE

Deletes all records but keeps the table structure.
TRUNCATE TABLE payroll;
<img width="961" height="205" alt="image" src="https://github.com/user-attachments/assets/5b1a660a-7757-40d2-bb91-fdb542f5bfab" />

# 2. DML (Data Manipulation Language)

DML commands are used to insert, update, and delete data.

1. INSERT

Adds new records.

INSERT INTO employees
(employee_id, first_name, last_name, department, salary)
VALUES
(104,'Rahul','Kumar','IT',55000);

<img width="954" height="317" alt="image" src="https://github.com/user-attachments/assets/eb4ba535-823e-4537-9ac3-64cfe9609ddf" />

2. UPDATE

Modifies existing records.
Increase Rahul's salary.

UPDATE employees
SET salary = 60000
WHERE employee_id = 104;

<img width="1243" height="297" alt="image" src="https://github.com/user-attachments/assets/967510f6-4010-426e-af4b-538cd186e318" />

3. DELETE

Deletes selected records.

DELETE FROM employees
WHERE employee_id = 104;

<img width="1223" height="291" alt="image" src="https://github.com/user-attachments/assets/2eed750b-ca0d-4448-a2bf-e649e60f9940" />

# 3. DQL (Data Query Language)

DQL is mainly used to retrieve data.

1.SELECT *
Display all employees.

SELECT *
FROM employees;

<img width="1112" height="522" alt="image" src="https://github.com/user-attachments/assets/4ce4b0b8-8925-4a0d-8b65-921823358531" />

2.SELECT Specific Columns
SELECT first_name,
       department
FROM employees;
<img width="784" height="470" alt="image" src="https://github.com/user-attachments/assets/92178503-2880-4da6-98ff-93d3dbe22317" />

3.WHERE

Retrieve employees in the IT department.

SELECT *
FROM employees
WHERE department = 'IT';

<img width="853" height="411" alt="image" src="https://github.com/user-attachments/assets/f1ce256b-2264-4aff-a436-d5cbfd4ba577" />


4.ORDER BY

Sort employees by salary.

SELECT *
FROM employees
ORDER BY salary DESC;

Highest salary appears first.

<img width="1005" height="404" alt="image" src="https://github.com/user-attachments/assets/bb6da6e2-f8a9-41c6-9041-c888ab5199f7" />

# 4. DCL (Data Control Language)

DCL commands manage permissions.

1.GRANT

Give read permission to another user.

GRANT SELECT
ON employees
TO hr_user;

2.REVOKE

Remove permission.

REVOKE SELECT
ON employees
FROM hr_user;

# 5. TCL (Transaction Control Language)

TCL commands manage transactions.

1.COMMIT

Save changes permanently.

UPDATE employees
SET salary = salary + 5000
WHERE department='HR';

COMMIT;

The salary update becomes permanent.

2.ROLLBACK

Undo changes before committing.

UPDATE employees
SET salary = salary + 5000
WHERE employee_id=101;

ROLLBACK;

The employee's salary returns to its previous value.

3.SAVEPOINT

Create a point within a transaction.

UPDATE payroll
SET net_salary = net_salary + 2000
WHERE employee_id=102;

SAVEPOINT salary_update;

If needed:

ROLLBACK TO salary_update;

Only changes made after the savepoint are undone.

# Retrieving Data in SQL
 Retrieving data means fetching information from one or more tables in a database. The main SQL command used for retrieving data is SELECT.
1.SELECT

The SELECT statement retrieves data from a table.

Syntax
SELECT column_name
FROM table_name;
Example 1: Display All Columns
SELECT *
FROM employees;
<img width="988" height="389" alt="image" src="https://github.com/user-attachments/assets/176fa2a2-d65e-4a72-b35c-14f8dfa98c32" />

Example 2: Display Specific Columns
SELECT first_name, department, salary
FROM employees;
<img width="774" height="394" alt="image" src="https://github.com/user-attachments/assets/4567f8e7-b5b3-4c7d-a418-f9334caf556c" />

2.DISTINCT

DISTINCT removes duplicate values.

Syntax
SELECT DISTINCT column_name
FROM table_name;
Example 1: List All Departments
SELECT DISTINCT department
FROM employees;
<img width="631" height="286" alt="image" src="https://github.com/user-attachments/assets/fe04f9d0-a5fa-4c96-a7bd-d9a1f9cbb1d7" />

3.WHERE

The WHERE clause filters rows based on a condition.

Syntax
SELECT column_name
FROM table_name
WHERE condition;
Example 1: Employees in IT Department
SELECT *
FROM employees
WHERE department = 'IT';
<img width="846" height="416" alt="image" src="https://github.com/user-attachments/assets/f2901894-8b07-4d4e-bb27-add7c315b8f9" />
Example 2: Employees with Salary Greater Than ₹50,000
SELECT first_name, salary
FROM employees
WHERE salary > 50000;
<img width="772" height="408" alt="image" src="https://github.com/user-attachments/assets/ae0cc300-08d8-4a1b-814e-acd259f6f5c1" />

4.ORDER BY

ORDER BY sorts the result in ascending (ASC) or descending (DESC) order.

Syntax
SELECT column_name
FROM table_name
ORDER BY column_name ASC;

or

SELECT column_name
FROM table_name
ORDER BY column_name DESC;
Example 1: Salary in Ascending Order
SELECT first_name, salary
FROM employees
ORDER BY salary ASC;
<img width="779" height="423" alt="image" src="https://github.com/user-attachments/assets/d2fccb3f-11a8-4e7e-b290-0e57ad8ca601" />

5.LIMIT

LIMIT restricts the number of rows returned.

Note: LIMIT is supported in MySQL and PostgreSQL. In SQL Server, use TOP.

Syntax
SELECT *
FROM employees
LIMIT 3;
Example 1: First 3 Employees
SELECT *
FROM employees
LIMIT 3;
<img width="953" height="295" alt="image" src="https://github.com/user-attachments/assets/6a7e8fee-ecce-4c61-9649-8caebcc48d0b" />
Example 2: Top 2 Highest Paid Employees
SELECT first_name, salary
FROM employees
ORDER BY salary DESC
LIMIT 2;
<img width="889" height="266" alt="image" src="https://github.com/user-attachments/assets/7deea494-e58e-44a9-9465-41bc17815e90" />

6.Aliases (AS)

An alias gives a temporary name to a column or table, making the output easier to read.
Column Alias
Syntax
SELECT column_name AS alias_name
FROM table_name;
Example 1
SELECT first_name AS Employee_Name,
       salary AS Monthly_Salary
FROM employees;
<img width="502" height="407" alt="image" src="https://github.com/user-attachments/assets/026b6d19-efdb-42c9-b26a-092306bd206e" />

Table Alias
SELECT e.first_name,
       e.salary
FROM employees AS e;
<img width="688" height="414" alt="image" src="https://github.com/user-attachments/assets/81b88cb2-bebd-4b86-bda8-ac8d1270d2b9" />




