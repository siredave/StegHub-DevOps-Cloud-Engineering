# Basic SQL Syntax and Commonly Used Commands

SQL (Structured Query Language) is used to communicate with databases. Below is a guide covering the basic syntax and some of the most commonly used SQL commands.

## 1. SELECT
The `SELECT` statement is used to query the database and retrieve data.

```sql
SELECT column1, column2, ...
FROM table_name;
```

**Example:**

```sql
SELECT first_name, last_name
FROM employees;
```

## 2. WHERE
The `WHERE` clause is used to filter records.

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

**Example:**

```sql
SELECT first_name, last_name
FROM employees
WHERE department = 'Sales';
```

## 3. INSERT INTO
The `INSERT INTO` statement is used to add new records to a table.

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

**Example:**

```sql
INSERT INTO employees (first_name, last_name, department)
VALUES ('John', 'Doe', 'Sales');
```

## 4. UPDATE
The `UPDATE` statement is used to modify existing records in a table.

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

**Example:**

```sql
UPDATE employees
SET department = 'Marketing'
WHERE last_name = 'Doe';
```

## 5. DELETE
The `DELETE` statement is used to delete records from a table.

```sql
DELETE FROM table_name
WHERE condition;
```

**Example:**

```sql
DELETE FROM employees
WHERE last_name = 'Doe';
```

## 6. CREATE TABLE
The `CREATE TABLE` statement is used to create a new table.

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    ...
);
```

**Example:**

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    department VARCHAR(50)
);
```

## 7. ALTER TABLE
The `ALTER TABLE` statement is used to add, delete, or modify columns in an existing table.

```sql
-- Add a column
ALTER TABLE table_name
ADD column_name datatype;

-- Drop a column
ALTER TABLE table_name
DROP COLUMN column_name;

-- Modify a column
ALTER TABLE table_name
MODIFY COLUMN column_name datatype;
```

**Example:**

```sql
-- Add a new column
ALTER TABLE employees
ADD birth_date DATE;

-- Drop a column
ALTER TABLE employees
DROP COLUMN birth_date;

-- Modify a column
ALTER TABLE employees
MODIFY COLUMN first_name VARCHAR(100);
```

## 8. DROP TABLE
The `DROP TABLE` statement is used to delete a table.

```sql
DROP TABLE table_name;
```

**Example:**

```sql
DROP TABLE employees;
```

## 9. JOIN
The `JOIN` clause is used to combine rows from two or more tables based on a related column.

```sql
-- INNER JOIN
SELECT columns
FROM table1
INNER JOIN table2
ON table1.common_column = table2.common_column;

-- LEFT JOIN
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.common_column = table2.common_column;

-- RIGHT JOIN
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.common_column = table2.common_column;

-- FULL JOIN
SELECT columns
FROM table1
FULL JOIN table2
ON table1.common_column = table2.common_column;
```

**Example:**

```sql
SELECT employees.first_name, departments.department_name
FROM employees
INNER JOIN departments
ON employees.department_id = departments.department_id;
```

## 10. GROUP BY
The `GROUP BY` statement is used to arrange identical data into groups.

```sql
SELECT column1, COUNT(*)
FROM table_name
GROUP BY column1;
```

**Example:**

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

## 11. HAVING
The `HAVING` clause is used to filter groups based on a specified condition.

```sql
SELECT column1, COUNT(*)
FROM table_name
GROUP BY column1
HAVING COUNT(*) > value;
```

**Example:**

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

## 12. ORDER BY
The `ORDER BY` clause is used to sort the result-set in ascending or descending order.

```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1 [ASC|DESC];
```

**Example:**

```sql
SELECT first_name, last_name
FROM employees
ORDER BY last_name ASC;
```

### Summary

These are the basic SQL commands and syntax that are commonly used for database operations. Mastering these commands will help you interact effectively with relational databases.
