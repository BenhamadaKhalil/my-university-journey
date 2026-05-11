## SQL Lesson Summary

### 1. **Introduction to SQL**
SQL (Structured Query Language) is used to manage relational databases. It is standardized by ANSI and ISO and is widely used in database management systems (DBMS).

- **Key Components of SQL:**
  - **DDL (Data Definition Language)**: Defines the database schema (structure).
  - **DML (Data Manipulation Language)**: Manipulates the data within the schema.
  - **DCL (Data Control Language)**: Controls access to the data.

### 2. **SQL Commands**

#### **A. Data Definition Language (DDL)**
- **Creating a Database**: 
```sql
  CREATE DATABASE <database_name>;
```


- **Dropping a Database**:
    
    ```sql
    DROP DATABASE <database_name>;
    ```
    
- **Creating a Table**: Defines the table’s structure.
    
    ```sql
    CREATE TABLE <table_name> (
        <column_name1> <column_type1> [<constraints>],
        ...
    );
    ```
    
- **Dropping a Table**: Deletes a table.
    
    ```sql
    DROP TABLE <table_name>;
    ```
    

#### **B. Data Manipulation Language (DML)**

- **SELECT**: Retrieves data from one or more tables.
    
    ```sql
    SELECT <column1>, <column2> FROM <table_name> WHERE <condition>;
    ```
    

#### **C. Data Control Language (DCL)**

- **Provides and removes access rights** (typically used for user permissions).
    

### 3. **Basic SQL Operations**

#### **A. Projection**

- Select specific columns (attributes).
    
    ```sql
    SELECT name, major FROM students;
    ```
    

#### **B. Cartesian Product**

- Combines every row from two tables, creating all possible combinations of rows.
    
    ```sql
    SELECT * FROM students, courses;
    ```
    

#### **C. Selection**

- Filters rows based on a specified condition.
    
    ```sql
    SELECT * FROM students WHERE age >= 20;
    ```
    

### 4. **Join Operations**

- **INNER JOIN**: Combines rows that have matching values in both tables.
    
    ```sql
    SELECT students.name, enrollments.grade
    FROM students
    INNER JOIN enrollments ON students.studentid = enrollments.studentid;
    ```
    
- **LEFT JOIN**: Retrieves all rows from the left table and matching rows from the right table.
    
- **RIGHT JOIN**: Retrieves all rows from the right table and matching rows from the left table.
    

### 5. **Aggregate Functions**

SQL provides several functions for summarizing data:

- **COUNT()**: Counts the number of rows.
    
    ```sql
    SELECT COUNT(studentid) FROM enrollments WHERE grade = 'A';
    ```
    
- **SUM()**, **AVG()**, **MIN()**, **MAX()**: Perform calculations on numeric data.
    

### 6. **Grouping Data with GROUP BY**

- **GROUP BY**: Groups rows that have the same values in specified columns.
    
    ```sql
    SELECT major, COUNT(studentid) FROM students GROUP BY major;
    ```
    
- **HAVING**: Filters groups based on a condition.
    
    ```sql
    SELECT major, COUNT(studentid) FROM students GROUP BY major HAVING COUNT(studentid) > 10;
    ```
    

### 7. **Subqueries (Nested Queries)**

- **Subqueries** are used inside the `WHERE` clause to filter results based on another query.
    
    ```sql
    SELECT name FROM students WHERE studentid IN (SELECT studentid FROM enrollments WHERE grade = 'A');
    ```
    

### 8. **Sorting Results with ORDER BY**

- **ORDER BY**: Sorts the results in ascending or descending order.
    
    ```sql
    SELECT name FROM students ORDER BY name ASC;
    ```
    

### 9. **Ensemblist Operations**

These operations combine results from multiple queries:

- **UNION**: Combines the results from two queries, removing duplicates.
    
- **INTERSECT**: Returns common rows between two queries.
    
- **MINUS**: Returns rows from the first query that are not in the second query.
    

Example:

```sql
SELECT studentid FROM enrollments WHERE grade = 'A'
UNION
SELECT studentid FROM enrollments WHERE grade = 'B';
```

### 10. **Division Operation**

The division operation returns rows from one table that are associated with all rows from another table. In SQL, this can be simulated using `GROUP BY` and `HAVING`.

```sql
SELECT studentid FROM enrollments
GROUP BY studentid
HAVING COUNT(courseid) = (SELECT COUNT(DISTINCT courseid) FROM enrollments);
```

### 11. **Calculation Functions**

- **SUM()**: Sums numeric values.
    
- **AVG()**: Calculates the average.
    
- **MIN()**, **MAX()**: Returns the minimum or maximum values.
    

Example:

```sql
SELECT AVG(price) FROM courses WHERE credits > 20;
```

### 12. **ORDER BY Clause**

Used to sort results in ascending (`ASC`) or descending (`DESC`) order:

```sql
SELECT name FROM students ORDER BY name DESC;
```

### 13. **Nested Queries (Nested SELECT)**

- **IN**: Checks if a value exists in a set returned by a subquery.
    
    ```sql
    SELECT name FROM students WHERE studentid IN (SELECT studentid FROM enrollments WHERE grade = 'A');
    ```
    
- **NOT IN**: Ensures a value does not exist in the set returned by a subquery.
    
- **EXISTS**: Returns TRUE if the subquery returns at least one result.
    

### Conclusion

SQL is an essential tool for working with relational databases, enabling users to create, manipulate, and query databases effectively. Mastering these commands and operations forms the foundation for efficient database management.
