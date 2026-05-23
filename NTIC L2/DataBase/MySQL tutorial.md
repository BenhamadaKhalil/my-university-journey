# 🏢 MAGASINS Database – SQL Documentation
## 🏗️ 1. Create the Database
-- Create the database
CREATE DATABASE MAGASINS;

-- Show all available databases
SHOW DATABASES;

-- Select the MAGASINS database
USE MAGASINS;

## 🧱 2. Create the Table: `magasin`
-- Create the "magasin" table with:
-- numM: primary key
-- adresse: required
-- superficie: default 100
CREATE TABLE magasin (
    numM INTEGER(5) PRIMARY KEY,
    adresse VARCHAR(25) NOT NULL,
    superficie INTEGER(5) DEFAULT 100
);

## 📂 3. View Table Information
 -- Show all tables in the current database
SHOW TABLES;

-- Describe the structure of the "magasin" table
DESCRIBE magasin;

## 📝 4. Insert Data into `magasin`
-- Insert a full row (all fields specified)
INSERT INTO magasin VALUES (1, 'Annaba', 300);

-- Insert row with default value for superficie
INSERT INTO magasin (numM, adresse) VALUES (2, 'Constantine');

## 🔍 5. Retrieve Data
-- Display all records in the "magasin" table
SELECT * FROM magasin;

## 🔧 6. Modify Table Structure
### ➕ Add a New Column: `typeM`
-- Add a new column for magasin type
ALTER TABLE magasin
ADD typeM VARCHAR(30);

### ✏️ Rename Column: `adresse` ➜ `adr`
-- Rename "adresse" to "adr" and change type to VARCHAR(200)
ALTER TABLE magasin
CHANGE adresse adr VARCHAR(200);

### ➖ Remove Column: `typeM`
-- Drop the "typeM" column
ALTER TABLE magasin
DROP COLUMN typeM;

### 🔄 Modify Column Type: `superficie`
-- Ensure "superficie" is correctly defined
ALTER TABLE magasin
MODIFY superficie INT(5);

## ✅ Final Check 
-- Confirm table structure and content
DESCRIBE magasin;
SELECT * FROM magasin;



# 👥 Employees Table – SQL Management
##  1.🧱 Create the `employees` Table
-- Create a table to store employee data
CREATE TABLE employees (
    employee_id INT,
    first_name VARCHAR(50),
    last_name VARCHAR(50), 
    hourly_pay DECIMAL(5, 2),
    hire_date DATE
);

##  2.🔍 View Table Contents
-- View all records in the employees table
SELECT * FROM employees;

##  3.📝  Rename the Table
-- Rename the table from 'employees' to 'workers'
RENAME TABLE employees TO workers;



##  4.❌  Drop the Table
-- Delete the 'employees' table entirely
DROP TABLE employees;

##  5.🛠️  Alter the Table Structure
### ➕ Add a New Column: `phone_number`
-- Add a phone_number column to the employees table
ALTER TABLE employees
ADD phone_number VARCHAR(15);

### ✏️ Rename Column: `phone_number` ➜ `email`
-- Rename 'phone_number' column to 'email'
ALTER TABLE employees
RENAME COLUMN phone_number TO email;

### 🔄 Modify Column Type: `email` to VARCHAR(100)
-- Change 'email' column type to allow longer values
ALTER TABLE employees
MODIFY COLUMN email VARCHAR(100);

### 📍 Reorder Column: Place `email` After `last_name`
-- Move the 'email' column after 'last_name'
ALTER TABLE employees 
MODIFY email VARCHAR(100) 
AFTER last_name;

### 🔝 Reorder Column: Place `email` First
-- Move the 'email' column to the first position
ALTER TABLE employees 
MODIFY email VARCHAR(100) 
FIRST;

### ➖ Remove the `email` Column
-- Drop the 'email' column from the table
ALTER TABLE employees
DROP COLUMN email;

##  6.🧪 Insert Examples – `employees` Table
### 📥 Example 1 – Insert a Single Record
-- Insert one employee into the employees table
INSERT INTO employees
VALUES (1, "Eugene", "Krabs", 25.50, "2023-01-02");

-- View the updated table
SELECT * FROM employees;

### 📥 Example 2 – Insert Multiple Records
-- Insert multiple employees at once
INSERT INTO employees
VALUES 
    (2, "Squidward", "Tentacles", 15.00, "2023-01-03"), 
    (3, "Spongebob", "Squarepants", 12.50, "2023-01-04"), 
    (4, "Patrick", "Star", 12.50, "2023-01-05"), 
    (5, "Sandy", "Cheeks", 17.25, "2023-01-06");

-- View the updated table
SELECT * FROM employees;

### 📥 Example 3 – Insert Partial Record (Some Columns)
-- Insert only ID, first name, and last name (nulls will be used for other columns)
INSERT INTO employees (employee_id, first_name, last_name)
VALUES (6, "Sheldon", "Plankton");

-- View the updated table
SELECT * FROM employees;


##  7.🔍SQL SELECT Queries – `employees` Table
### 📋 1. Select All Columns
-- Select all columns from the employees table
SELECT * FROM employees;

### 🧑‍🤝‍🧑 2. Select `first_name` and `last_name`
-- Select only the first name and last name columns
SELECT first_name, last_name FROM employees;

### 🔄 3. Select `last_name` and `first_name` (Swapped Order)
-- Select last name and first name in swapped order
SELECT last_name, first_name FROM employees;

### 🔎 4. Select by `employee_id`
-- Select employee where employee_id is 1
SELECT *
FROM employees
WHERE employee_id = 1;

### 💡 5. Select by `first_name`
-- Select employee where first name is "Spongebob"
SELECT *
FROM employees
WHERE first_name = "Spongebob";

### 💰 6. Select Employees with `hourly_pay` >= 15
-- Select employees with an hourly pay greater than or equal to 15
SELECT *
FROM employees
WHERE hourly_pay >= 15;

### 📅 7. Select by `hire_date`
-- Select employees hired on or before 2023-01-03
SELECT hire_date, first_name
FROM employees
WHERE hire_date <= "2023-01-03";

### ❌ 8. Select Employees Excluding a Specific `employee_id`
-- Select employees where employee_id is not 1
SELECT *
FROM employees
WHERE employee_id != 1;

### 🚫 9. Select Employees with `NULL` `hire_date`
-- Select employees where hire_date is NULL
SELECT *
FROM employees
WHERE hire_date IS NULL;

### ✅ 10. Select Employees with `NOT NULL` `hire_date`
-- Select employees where hire_date is not NULL
SELECT *
FROM employees
WHERE hire_date IS NOT NULL;


##  8.🛠️ SQL UPDATE and DELETE Queries – `employees` Table

### ✏️ 1. Update Employee Pay
-- Update the hourly pay for the employee with employee_id = 6
UPDATE employees
SET hourly_pay = 10.25
WHERE employee_id = 6;

-- View the updated table
SELECT * FROM employees;

### ❌ 2. Delete Employee Record
-- Delete the employee with employee_id = 6
DELETE FROM employees
WHERE employee_id = 6;

-- View the updated table
SELECT * FROM employees;


##  9.💼 MySQL Transaction Control – `AUTOCOMMIT`, `COMMIT`, `ROLLBACK`

### 📝 1. AUTOCOMMIT Mode
-- Enable AUTOCOMMIT mode (default behavior)
-- Each SQL statement is automatically committed after it is executed
SET autocommit = 1;

-- Disable AUTOCOMMIT mode (manual commit needed)
-- Changes are not committed until explicitly done with COMMIT
SET autocommit = 0;

-- *Explanation*:

- **AUTOCOMMIT** is typically enabled by default, meaning every individual SQL query is automatically committed to the database.
    
- If **AUTOCOMMIT** is set to `0`, MySQL enters **manual commit mode**, where changes are only saved when `COMMIT` is explicitly called.
### ✔️ 2. COMMIT
-- Commit the current transaction (save all changes made since the last COMMIT)
COMMIT;

- Explanation:

- `COMMIT` is used to **make changes permanent** in the database. When you run `COMMIT`, all changes made since the last `COMMIT` (or since the start of the transaction) are saved.

### 🔙 3. ROLLBACK
-- Rollback the current transaction (undo all changes made since the last COMMIT)
ROLLBACK;

- Explanation:

- `ROLLBACK` is used to **undo changes** made during the current transaction. Any updates, inserts, or deletes performed since the last `COMMIT` will be reverted.

### Example of a Transaction with `COMMIT` and `ROLLBACK`:
-- Start a transaction (when autocommit is OFF)
START TRANSACTION;

-- Perform some updates
UPDATE employees
SET hourly_pay = 12.00
WHERE employee_id = 1;

-- Check if everything is okay before committing
SELECT * FROM employees WHERE employee_id = 1;

-- If everything looks good, commit the changes
COMMIT;

-- OR, if something went wrong, roll back the transaction
-- ROLLBACK;

--**Notes:

- Transactions help ensure that a sequence of operations is executed completely or not at all.
    
- For example, if you’re transferring money between two accounts, you would use `START TRANSACTION`, `COMMIT` when both accounts are updated correctly, or `ROLLBACK` if there's an error in one of the updates.

##  10.📅 MySQL Date and Time Data Types

### 🛠️ 1. Create `test` Table
-- Create a table with DATE, TIME, and DATETIME columns
CREATE TABLE test(
     my_date DATE,       -- Column to store the date
     my_time TIME,       -- Column to store the time
     my_datetime DATETIME  -- Column to store both date and time
);

### 📝 2. Insert Current Date, Time, and Datetime
-- Insert current date, time, and datetime into the table
INSERT INTO test
VALUES (CURRENT_DATE(), CURRENT_TIME(), NOW());

### 🔍 3. View the Data
-- Select all data from the test table to see the inserted values
SELECT * FROM test;
###
--📝 Explanation:

- **`CURRENT_DATE()`**: Returns the current date in `YYYY-MM-DD` format.
    
- **`CURRENT_TIME()`**: Returns the current time in `HH:MM:SS` format.
    
- **`NOW()`**: Returns the current date and time in `YYYY-MM-DD HH:MM:SS` format.


##  11.🔑 SQL `UNIQUE` Constraint

### 📝 1. What is the `UNIQUE` Constraint?

The **`UNIQUE` constraint** ensures that all values in a column are **distinct** or **unique** across the table. This means no two rows can have the same value in the column that has the `UNIQUE` constraint. The constraint can be applied to one or more columns.

- **Single Column**: When applied to a single column, it ensures no duplicate values in that column.
    
- **Multiple Columns**: When applied to a combination of columns, the combination of values across those columns must be unique.

### 🛠️ 2. Example of `UNIQUE` Constraint on a Single Column
-- Create the products table with a UNIQUE constraint on the product_name column
CREATE TABLE products (
    product_id INT,                -- Column for product ID
    product_name VARCHAR(25) UNIQUE, -- Enforcing uniqueness for the product_name column
    price DECIMAL(4, 2)            -- Column for product price
);

- Explanation:

- **`product_name`**: The `UNIQUE` constraint ensures that no two products can have the same name in the `product_name` column.

### 🧑‍🍳 3. Example of Inserting Data with the `UNIQUE` Constraint
-- Insert data into the products table
INSERT INTO products
VALUES (100, 'hamburger', 3.99),
               (101, 'fries', 1.89),
               (102, 'soda', 1.00),
               (103, 'ice cream', 1.49);

- **Attempting to Insert Duplicate Product Names**: If you try to insert a product with a duplicate name (e.g., another "hamburger"), it will result in an error, because the `product_name` column is **unique**.

### 🔧 4. Adding a `UNIQUE` Constraint to an Existing Column
-- Add a UNIQUE constraint on the product_name column
ALTER TABLE products
ADD CONSTRAINT
UNIQUE (product_name);

##  12.🔑 SQL `CHECK` Constraint

### 📝 1. What is the `CHECK` Constraint?

The **`CHECK` constraint** is used to limit the range of values that can be entered into a column. It ensures that values in a column satisfy a specific condition, and if the condition is not met, the insertion or update is rejected.

- It can be used for **single column checks** (e.g., ensuring a column's value falls within a certain range).
    
- It can also be used for **multiple column checks** (e.g., ensuring that two columns must satisfy certain conditions together).

### 🛠️ 2. Example of `CHECK` Constraint on a Single Column
-- Create a table with a CHECK constraint on the price column
CREATE TABLE products (
    product_id INT,                  -- Column for product ID
    product_name VARCHAR(50),         -- Column for product name
    price DECIMAL(5, 2),              -- Column for price
    CHECK (price >= 0)                -- Price must be greater than or equal to 0
);

-- **Explanation:

- The `CHECK` constraint on the `price` column ensures that the price cannot be **negative**. Only positive or zero values are allowed.

### 🧑‍🍳 3. Example of Inserting Data with the `CHECK` Constraint
-- Insert valid data into the products table
INSERT INTO products
VALUES (100, 'hamburger', 3.99), 
       (101, 'fries', 1.89),
       (102, 'soda', 1.00);

-- Attempting to insert invalid data (price < 0)
-- This will fail due to the CHECK constraint
INSERT INTO products
VALUES (103, 'ice cream', -1.49);

- In the second `INSERT` statement, trying to insert a product with a negative price will **fail**, as the `CHECK` constraint is enforcing that price values must be `>= 0`.

### 🔧 4. Adding a `CHECK` Constraint to an Existing Table
-- Add a CHECK constraint to ensure that price is greater than or equal to 0
ALTER TABLE products
ADD CONSTRAINT price_check
CHECK (price >= 0);

-- **Explanation:

- This command adds a constraint called `price_check` that enforces the condition that all values in the `price` column must be greater than or equal to zero.

### 📝 Key Points:

- The **`CHECK` constraint** is used to limit the range of valid values for a column or set of columns.
    
- The condition in a `CHECK` constraint can use **logical expressions**, such as `>=`, `<=`, `>`, `<`, `=` (equals), and `<>` (not equal).
    
- The **`CHECK` constraint** is enforced during `INSERT` and `UPDATE` operations.
    
- Some database systems (like older versions of MySQL) might ignore the `CHECK` constraint, so always verify compatibility with your DBMS.

##  13.🔑 SQL `PRIMARY KEY` Constraint

### 📝 1. What is the `PRIMARY KEY` Constraint?

The **`PRIMARY KEY`** constraint is used to uniquely identify each record in a table. It ensures that the column (or a combination of columns) contains **unique values** and **cannot be `NULL`**. A table can only have one `PRIMARY KEY`.

- **Uniqueness**: All values in the `PRIMARY KEY` column must be distinct.
    
- **Non-Null**: The `PRIMARY KEY` column(s) cannot have `NULL` values.
    
- **Single Column or Composite Key**: A `PRIMARY KEY` can be defined on a single column, or multiple columns can be used together to form a **composite primary key**.

### 🛠️ 2. Example of `PRIMARY KEY` on a Single Column
-- Create a products table with a PRIMARY KEY on the product_id column
CREATE TABLE products (
    product_id INT PRIMARY KEY,        -- The product_id is the PRIMARY KEY
    product_name VARCHAR(50),          -- Column for product name
    price DECIMAL(5, 2)                -- Column for product price
);

-- **Explanation:

- The **`PRIMARY KEY`** is placed on the `product_id` column, ensuring that each product has a **unique** and **non-null** `product_id`.

### 🧑‍🍳 3. Example of Inserting Data with a `PRIMARY KEY`
-- Insert data into the products table
INSERT INTO products (product_id, product_name, price)
VALUES (100, 'hamburger', 3.99),
       (101, 'fries', 1.89),
       (102, 'soda', 1.00);

-- Attempting to insert a duplicate product_id will fail
INSERT INTO products (product_id, product_name, price)
VALUES (100, 'ice cream', 1.49);  -- This will fail because product_id 100 already exists

- The **second `INSERT` statement** will fail, as the `PRIMARY KEY` constraint enforces uniqueness on the `product_id` column.

###  🔧 4. Example of `PRIMARY KEY` with a Composite Key (Multiple Columns)

-- Create an order_items table with a composite PRIMARY KEY (order_id, product_id)
CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT,
    PRIMARY KEY (order_id, product_id)   -- Composite PRIMARY KEY on order_id and product_id
);

-- **Explanation:

- The `PRIMARY KEY` is applied to the combination of `order_id` and `product_id`, ensuring that each pair of `order_id` and `product_id` is unique in the `order_items` table.

### 🛠️ 5. Adding a `PRIMARY KEY` to an Existing Table
-- If a table already exists and you want to add a `PRIMARY KEY` to one or more columns, you can use the `ALTER TABLE` statement:

-- Add a PRIMARY KEY to the product_id column
ALTER TABLE products
ADD PRIMARY KEY (product_id);

### 📝 Key Points:

- A **`PRIMARY KEY`** uniquely identifies each record in a table.
    
- A table can only have **one** `PRIMARY KEY`, but the `PRIMARY KEY` can consist of multiple columns, known as a **composite key**.
    
- The **`PRIMARY KEY`** ensures that the column(s) have **unique** values and cannot contain `NULL` values.
    
- A **composite key** is useful when no single column can uniquely identify a row on its own (e.g., in junction tables or relationship tables).


## 14.🧑‍🤝‍🧑 SQL `FOREIGN KEY` Constraints
### 🛠️ 1. Create `customers` Table
-- Create a customers table with auto-increment primary key
CREATE TABLE customers (
     customer_id INT PRIMARY KEY AUTO_INCREMENT,  -- Auto-increment primary key
     first_name VARCHAR(50),                       -- Column for the first name
     last_name VARCHAR(50)                         -- Column for the last name
);
-- **Explanation:

- The `customer_id` column is set as the **primary key** and will **auto-increment** with each new customer.

### 🧑‍🍳 2. Insert Data into `customers` Table
-- Insert sample customer data
INSERT INTO customers (first_name, last_name)
VALUES  ("Fred", "Fish"),
        ("Larry", "Lobster"),
        ("Bubble", "Bass");

### 🔍 3. View Data from `customers` Table
-- Select all data from the customers table
SELECT * FROM customers;

### 🛠️ 4. Create `transactions` Table with Foreign Key
-- Create a transactions table with a foreign key referencing the customers table
CREATE TABLE transactions (
    transaction_id INT PRIMARY KEY AUTO_INCREMENT,  -- Auto-increment primary key for transaction
    amount DECIMAL(5, 2),                           -- Column for the transaction amount
    customer_id INT,                                -- Column for customer ID (foreign key)
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)  -- Foreign key constraint
);

-- **Explanation:

- The `customer_id` column in the **`transactions`** table is a **foreign key** that references the `customer_id` in the **`customers`** table, creating a relationship between the two tables.
### 🔧 5. Set `AUTO_INCREMENT` for `transactions` Table
-- Set the starting point for the auto-increment in the transactions table
ALTER TABLE transactions
AUTO_INCREMENT = 1000;

-- **Explanation:

- This sets the starting value of the `transaction_id` auto-increment to **1000**.

### 🛠️ 6. Add Foreign Key to an Existing Table (`customers`)
-- Add a named foreign key constraint to the customers table
ALTER TABLE customers
ADD CONSTRAINT fk_customer_id
FOREIGN KEY (customer_id) REFERENCES customers(customer_id);

-- **Explanation:

- This command attempts to add a **foreign key** to the `customers` table, but since `customer_id` is already the primary key in that table, this would typically be unnecessary. However, this is just an example of adding a foreign key to an existing table.

### 📝 Key Points:

- The **`FOREIGN KEY`** constraint is used to establish a relationship between two tables.
    
- It ensures referential integrity, meaning the value in the foreign key column must exist in the referenced table (in this case, the `customer_id` in the `customers` table).
    
- **Auto-increment** is used to automatically generate unique values for primary key columns (e.g., `transaction_id` and `customer_id`).
    
- **Named constraints** (like `fk_customer_id`) are useful for clarity, especially in more complex databases.

---
## 🔗 Navigation
- **Module:** [[DataBase|◀ DataBase]]
- **Semester:** [[NTIC L2|◀ NTIC L2]]
- **Academic Home:** [[README|🏠 Home]]
