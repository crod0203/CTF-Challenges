# Command Snippets — Labs 6 & 7 (SQL Querying & Filtering)

> Safe, sanitized SQL examples and terminal commands from Labs 6 and 7.  
> **Important:** Replace table/column names with placeholders (`employees`, `sales`, etc.) for your dataset.  
> All examples are for educational use only.

---

## 1️⃣ Basic Selection
```sql
-- Select all columns
SELECT * FROM employees;

-- Select specific columns
SELECT first_name, last_name, salary FROM employees;
2️⃣ Filtering Rows with WHERE
-- Return rows where salary exceeds 50 000
SELECT first_name, salary FROM employees WHERE salary > 50000;

-- Find employees in the 'IT' department
SELECT * FROM employees WHERE department = 'IT';
3️⃣ Exclusionary Filtering
-- Exclude employees from the HR department
SELECT * FROM employees WHERE department <> 'HR';

-- Exclude specific IDs
SELECT * FROM employees WHERE id NOT IN (1, 5, 9);

4️⃣ Combining Conditions with AND / OR
-- Multiple conditions
SELECT * FROM employees WHERE department = 'IT' AND salary > 60000;

-- Either condition matches
SELECT * FROM employees WHERE department = 'Finance' OR department = 'Accounting';

5️⃣ Filtering Strings with LIKE
-- Names that start with 'A'
SELECT * FROM customers WHERE name LIKE 'A%';

-- Emails that contain '@example.com'
SELECT email FROM customers WHERE email LIKE '%@example.com';

6️⃣ Filtering on Expressions
-- Find employees earning more than the average
SELECT first_name, salary FROM employees 
WHERE salary > (SELECT AVG(salary) FROM employees);

-- Give everyone a 10% raise for display only
SELECT first_name, salary * 1.10 AS new_salary FROM employees;

7️⃣ Selecting Expressions & Derived Columns
-- Display full name and annual pay
SELECT first_name || ' ' || last_name AS full_name,
       salary * 12 AS annual_salary
FROM employees;

8️⃣ Composite Conditions
-- Combine multiple conditions using parentheses
SELECT * FROM employees
WHERE (department = 'IT' AND salary > 50000)
    OR (department = 'Finance' AND salary > 60000);

9️⃣ Reaching Your Limits (Restrict Result Set)
-- Return only the top 10 highest-paid employees
SELECT first_name, last_name, salary
FROM employees
ORDER BY salary DESC
LIMIT 10;

🔟 Querying Metadata
-- List all tables in the database
SHOW TABLES;

-- Describe a table's columns and types
DESCRIBE employees;

-- SQLite specific metadata
.tables
.schema employees

⚙️ Command-Line Database Helpers (Bash / Terminal)
# enter SQLite shell
sqlite3 company.db

# show tables quickly
.tables

# quit SQLite
.quit

# export query output to a CSV file
sqlite3 company.db ".mode csv" ".output employees.csv" "SELECT * FROM employees;"
