---
title: "MySql"
date: 2019-06-16
weight: 3
---

MySQL is an open-source relational database management system (RDBMS) that's used to store and manage data

![Accounting Services](/images/MySql/MySql.jpg)

# What is the difference between CHAR and VARCHAR data types?

- CHAR is a fixed-length data type. If you define a column as CHAR(10), it will always occupy 10 characters, padding with spaces if the data is shorter.
- VARCHAR is a variable-length data type. It stores only the characters you enter, plus one or two bytes to store the length of the string.
Use CHAR for fixed-length data like phone numbers or ZIP codes, and VARCHAR for variable-length strings like names or addresses.

# What are the different types of JOINs in MySQL?

- **INNER JOIN**: Returns records that have matching values in both tables.

```sql
SELECT columns FROM table1 INNER JOIN table2 ON table1.column = table2.column 
```

- **LEFT (OUTER) JOIN**: Returns all records from the left table, and the matched records from the right table. If no match, NULL is returned.

```sql
SELECT columns FROM table1 LEFT JOIN table2 ON table1.column = table2.column;
```

- **RIGHT (OUTER) JOIN**: Returns all records from the right table, and the matched records from the left table. If no match, NULL is returned.

```sql
SELECT columns FROM table1 RIGHT JOIN table2 ON table1.column = table2.column;
```

- **FULL (OUTER) JOIN**: Returns all records when there is a match in either left or right table. (MySQL does not support this directly, but it can be simulated using a UNION of LEFT JOIN and RIGHT JOIN.)

```sql
SELECT columns
FROM table1
LEFT JOIN table2 ON table1.column = table2.column
UNION
SELECT columns
FROM table1
RIGHT JOIN table2 ON table1.column = table2.column;
```

# How do you optimize a MySQL query?

- **Use Indexes**: Adding indexes on columns that are used in WHERE, JOIN, or ORDER BY clauses can speed up query performance.
- **Avoid SELECT (*)**: Selecting only the needed columns reduces the amount of data being retrieved and processed.
- **Query Caching**: Enable query caching to reuse the result set of previous queries.
- **Use EXPLAIN**: To understand how MySQL executes the query and identify performance bottlenecks.
- **Avoid using functions** in WHERE clauses, as it can prevent index usage.

# What is a Primary Key, and can a table have more than one Primary Key?

- A Primary Key is a unique identifier for each record in a table. It must contain **unique** values and cannot contain NULL.
- A table cannot have more than one primary key. However, you can create a **composite primary key**, which is made up of more than one column.

# What is the difference between WHERE and HAVING clauses?

- **WHERE** is used to filter records before grouping or aggregation occurs. It cannot be used with aggregate functions.
- **HAVING** is used to filter records after the aggregation has been performed. It can be used with aggregate functions.
Example:

```sql
SELECT department, COUNT(*)
FROM employees
WHERE salary > 50000
GROUP BY department
HAVING COUNT(*) > 5;
```

# Write a query to find the second-highest salary from an employees table.

```sql
SELECT MAX(salary)
FROM employee
WHERE salary < (SElECT MAX(SALARY) FROM employee)
```

### Query to Get the n-th Highest Record

```sql
SELECT salary
FROM employees e1
WHERE (n-1) = (
    SELECT COUNT(DISTINCT e2.salary)
    FROM employees e2
    WHERE e2.salary > e1.salary
)
```

# What is a VIEW in MySQL and when would you use it?

- A VIEW is a virtual table that is based on the result of a SELECT query. It does not store data itself but provides a way to encapsulate complex queries.
- Use a view to simplify data access, restrict access to certain data, or create reusable query logic.

```sql
CREATE VIEW high_salary_employees AS 
SELECT name, salary 
FROM employees 
WHERE salary > 100000;
)
```

# What is the difference between DELETE, TRUNCATE, and DROP?

- **DELETE**: Removes rows from a table based on the WHERE condition. It can be rolled back if within a transaction.

```sql
DELETE FROM table_name WHERE condition;
```

- **TRUNCATE**: Removes all rows from a table. It is faster than DELETE and resets the table’s auto-increment counter. It cannot be rolled back.

```sql
TRUNCATE TABLE table_name;
```

- **DROP**: Removes the entire table structure from the database. All data, indexes, and table definitions are deleted, and this operation cannot be rolled back.

```sql
DROP TABLE table_name;
```

# What is a FOREIGN KEY in MySQL?

- A Foreign Key is a field (or collection of fields) in one table that uniquely identifies a row of another table. It creates a relationship between two tables, ensuring referential integrity.

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```

# Explain the use of the EXPLAIN keyword in MySQL.

- **EXPLAIN** is used to obtain details about how MySQL executes a query. It provides insights into the query execution plan, showing how tables are accessed, the types of joins used, the use of indexes, and more.

```sql
EXPLAIN SELECT * FROM employees WHERE department_id = 5;
```
