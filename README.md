# SQL Cheatsheet

## 1. Basic SQL Syntax

### Select Data
```sql
SELECT column1, column2, ... FROM table_name;
```
- Select all columns:
  ```sql
  SELECT * FROM table_name;
  ```

### Filtering Data
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```
- Example:
  ```sql
  SELECT * FROM employees WHERE salary > 50000;
  ```

### Logical Operators
- **AND**: Combines conditions.
  ```sql
  SELECT * FROM employees WHERE salary > 50000 AND age < 30;
  ```
- **OR**: Returns records if either condition is true.
  ```sql
  SELECT * FROM employees WHERE salary > 50000 OR age < 30;
  ```
- **NOT**: Reverses the result.
  ```sql
  SELECT * FROM employees WHERE NOT (salary > 50000);
  ```

## 2. Sorting Data
```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column_name [ASC|DESC];
```
- Default sorting is **ASC** (ascending), use **DESC** for descending.
  ```sql
  SELECT * FROM employees ORDER BY salary DESC;
  ```

## 3. Limiting Results
```sql
SELECT column1, column2, ...
FROM table_name
LIMIT number;
```
- Example:
  ```sql
  SELECT * FROM employees LIMIT 5;
  ```

## 4. Aggregate Functions

### COUNT()
```sql
SELECT COUNT(*) FROM employees;
```

### SUM()
```sql
SELECT SUM(salary) FROM employees;
```

### AVG()
```sql
SELECT AVG(salary) FROM employees;
```

### MIN() / MAX()
```sql
SELECT MIN(salary), MAX(salary) FROM employees;
```

### GROUP BY
```sql
SELECT column_name, COUNT(*) 
FROM table_name
GROUP BY column_name;
```
- Example:
  ```sql
  SELECT department, COUNT(*) FROM employees GROUP BY department;
  ```

## 5. Joins

### INNER JOIN (Returns records with matching values in both tables)
```sql
SELECT columns
FROM table1
INNER JOIN table2 ON table1.column = table2.column;
```

### LEFT JOIN (Returns all records from the left table, and matching records from the right table)
```sql
SELECT columns
FROM table1
LEFT JOIN table2 ON table1.column = table2.column;
```

### RIGHT JOIN (Returns all records from the right table, and matching records from the left table)
```sql
SELECT columns
FROM table1
RIGHT JOIN table2 ON table1.column = table2.column;
```

### FULL JOIN (Returns records when there is a match in either left or right table)
```sql
SELECT columns
FROM table1
FULL JOIN table2 ON table1.column = table2.column;
```

## 6. Subqueries

### Subquery in SELECT
```sql
SELECT column1, (SELECT column FROM table2 WHERE condition)
FROM table1;
```

### Subquery in WHERE
```sql
SELECT column1
FROM table1
WHERE column2 = (SELECT column FROM table2 WHERE condition);
```

## 7. Modifying Data

### INSERT
```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```
- Example:
  ```sql
  INSERT INTO employees (name, salary) VALUES ('John Doe', 60000);
  ```

### UPDATE
```sql
UPDATE table_name
SET column1 = value1, column2 = value2
WHERE condition;
```
- Example:
  ```sql
  UPDATE employees SET salary = 70000 WHERE name = 'John Doe';
  ```

### DELETE
```sql
DELETE FROM table_name WHERE condition;
```
- Example:
  ```sql
  DELETE FROM employees WHERE name = 'John Doe';
  ```

## 8. Creating and Managing Tables

### CREATE TABLE
```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    ...
);
```
- Example:
  ```sql
  CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    salary DECIMAL(10, 2)
  );
  ```

### ALTER TABLE (Modify an existing table)

#### Add a column
```sql
ALTER TABLE table_name ADD column_name datatype;
```
#### Drop a column
```sql
ALTER TABLE table_name DROP COLUMN column_name;
```
#### Modify a column
```sql
ALTER TABLE table_name MODIFY column_name new_datatype;
```

### DROP TABLE
```sql
DROP TABLE table_name;
```

## 9. Constraints

- **PRIMARY KEY**: Uniquely identifies each record.
  ```sql
  CREATE TABLE employees (
      id INT PRIMARY KEY,
      name VARCHAR(100)
  );
  ```

- **FOREIGN KEY**: Ensures referential integrity between tables.
  ```sql
  CREATE TABLE orders (
      order_id INT PRIMARY KEY,
      customer_id INT,
      FOREIGN KEY (customer_id) REFERENCES customers(id)
  );
  ```

- **NOT NULL**: Ensures that a column cannot have a NULL value.
  ```sql
  CREATE TABLE employees (
      id INT PRIMARY KEY,
      name VARCHAR(100) NOT NULL
  );
  ```

- **UNIQUE**: Ensures that all values in a column are different.
  ```sql
  CREATE TABLE employees (
      id INT PRIMARY KEY,
      email VARCHAR(100) UNIQUE
  );
  ```

- **CHECK**: Ensures that values meet a certain condition.
  ```sql
  CREATE TABLE employees (
      id INT PRIMARY KEY,
      age INT CHECK (age >= 18)
  );
  ```

## 10. Indexes
Indexes are used to speed up the retrieval of rows from a database table.
```sql
CREATE INDEX index_name ON table_name (column_name);
```
- Example:
  ```sql
  CREATE INDEX idx_salary ON employees (salary);
  ```

## 11. Transactions

### Begin a Transaction
```sql
BEGIN;
```

### Commit a Transaction
```sql
COMMIT;
```

### Rollback a Transaction
```sql
ROLLBACK;
```

## 12. Views
A **view** is a virtual table based on the result of a SELECT query.
```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

- Example:
  ```sql
  CREATE VIEW high_salary_employees AS
  SELECT * FROM employees WHERE salary > 60000;
  ```
