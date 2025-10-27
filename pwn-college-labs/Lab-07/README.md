# 🧮 Labs 6 & 7 — SQL Querying & Filtering Data

**Name:** Carlos Rodriguez  
**Course:** CSCI 400 (Section 01)  
**pwn.college Username:** Carlos  
**Source:** Original lab notes and exercises (sanitized).    

---

## 🎯 Objecti fundamental **SQL querying and filtering** techniques for working with tabular data.  
Through multiple practice queries, I learned how to:
- select specific columns,  
- filter rows using `WHERE` conditions,  
- apply logical operators (`AND`, `OR`, `NOT`),  
- use pattern matching (`LIKE`, `%`, `_`), and  
- explore database metadata to better understand schema structure.  

---

## 🧩 Lab 6 — Filtering & Selecting Columns
**Topics Covered**
- Writing basic `SELECT` statements to retrieve data from tables.  
- Limiting output with specific columns (`SELECT column1, column2 FROM table;`).  
- Filtering rows using simple conditions (`WHERE salary > 50000`).  
- Excluding records with `NOT` or inequality operators (`<, > , !=`).  
- Combining conditions for precise queries (`AND`, `OR`).  

**Example Concepts**
- **Filtering SQL:** Return only records that match defined criteria.  
- **Choosing Columns:** Show only relevant fields to reduce output.  
- **Exclusionary Filtering:** Omit data by using `NOT IN` or `<>`.  

---

## 🧩 Lab 7 — Advanced Filtering & Expressions
**Topics Covered**
- **Filtering Strings:** Use `LIKE` with wildcards for pattern matching.  
- **Filtering on Expressions:** Perform calculations in queries (e.g., `salary * 1.1 AS new_salary`).  
- **Selecting Expressions:** Display derived values directly in the output.  
- **Composite Conditions:** Combine multiple logical checks using `AND` / `OR` chains for multi-criteria queries.  
- **Reaching Your Limits:** Use `LIMIT` to restrict result set size for large tables.  
- **Querying Metadata:** Investigate database schema information (e.g., `SHOW TABLES;`, `DESCRIBE table;`).  

---

## 🧰 Tools & Commands Practiced
- SQL Shell (MySQL / SQLite / PostgreSQL)  
- `SELECT`, `FROM`, `WHERE`, `ORDER BY`, `LIMIT`, `DISTINCT`  
- Arithmetic and string expressions inside queries  
- Schema introspection commands (`.tables`, `.schema`, `SHOW TABLES;`)  

---

## ✅ Key Takeaways
- SQL filters and expressions make data retrieval precise and efficient.  
- Logical operators and wildcards enable flexible searching.  
- Derived columns (through expressions and aliases) help analyze data on the fly.  
- Understanding metadata improves query planning and schema awareness.  

---

## 📁 Files in this Folder
lab-06_07/
├── Carlos-Rodriguez-Lab6_7.pdf # Full sanitized lab report (screenshots included)
├── README.md # This summary file
└── COMMAND-SNIPPETS.md # SQL examples and commands

---

⭐ *These labs built my foundation in SQL query construction and data filtering — skills essential for cybersecurity analysis and data-driven investigations.*
