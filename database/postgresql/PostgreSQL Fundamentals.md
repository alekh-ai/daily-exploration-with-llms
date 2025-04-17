# PostgreSQL Fundamentals

## Chapter 1: Introduction to PostgreSQL

### 1.1 What is PostgreSQL?
PostgreSQL, often referred to as "Postgres," is a robust, open-source, object-relational database management system (ORDBMS). It is renowned for its reliability, extensive feature set, and strong adherence to SQL standards.

### 1.2 Why Choose PostgreSQL?
* **Open Source and Free:** No licensing fees, promoting accessibility.
* **Extensibility:** Allows users to define custom functions, data types, and operators.
* **Advanced Features:** Supports ACID-compliant transactions, concurrency control (MVCC), views, stored procedures, and triggers.
* **Scalability:** Capable of handling large datasets and high transaction volumes.
* **Strong Community Support:** Benefit from a large and active community providing excellent documentation and assistance.
* **SQL Standard Compliance:** Adheres closely to SQL standards, ensuring portability.
* **Data Integrity:** Offers robust mechanisms for maintaining data consistency and reliability.

### 1.3 Use Cases
PostgreSQL is employed in diverse applications, ranging from web development and mobile backends to geospatial analysis and scientific research.

## Chapter 2: Core Database Concepts

### 2.1 Databases
A database serves as a structured container for organizing and managing related data. A single PostgreSQL server can host multiple independent databases.

### 2.2 Schemas
Within a database, schemas act as namespaces to logically group database objects such as tables, views, and functions. The default schema is typically named `public`.

### 2.3 Tables
Tables are the fundamental units of data storage, consisting of rows and columns. Each table holds data about a specific entity.

### 2.4 Columns
Columns define the attributes of the entity stored in a table. Each column has a name and a specific data type.

### 2.5 Rows (Tuples)
A row represents a single instance or record of the entity described by the table. It contains values for each of the table's columns.

### 2.6 Data Types
Data types specify the kind of data that can be stored in a column, ensuring data integrity and efficient storage.

## Chapter 3: Interacting with PostgreSQL

### 3.1 Connecting with `psql`
`psql` is the command-line interface for PostgreSQL, allowing direct interaction with the database server.

* **Basic Connection:**
    ```bash
    psql
    ```
* **Connecting to a Specific Database and User:**
    ```bash
    psql -d <database_name> -U <username>
    ```
* **Exiting `psql`:**
    ```sql
    \q
    ```

## Chapter 4: Basic SQL Queries

### 4.1 Data Definition Language (DDL)
Used to define and manage the structure of database objects.

* **`CREATE DATABASE`:** Creates a new database.
    ```sql
    CREATE DATABASE my_first_database;
    ```
* **`CREATE SCHEMA`:** Creates a new schema.
    ```sql
    CREATE SCHEMA my_schema;
    ```
* **`CREATE TABLE`:** Creates a new table.
    ```sql
    CREATE TABLE customers (
        customer_id SERIAL PRIMARY KEY,
        first_name VARCHAR(50) NOT NULL,
        last_name VARCHAR(50),
        email VARCHAR(100) UNIQUE,
        registration_date DATE DEFAULT CURRENT_DATE
    );
    ```
* **`ALTER DATABASE`:** Modifies a database.
    ```sql
    ALTER DATABASE my_first_database RENAME TO new_database_name;
    ```
* **`ALTER SCHEMA`:** Modifies a schema.
    ```sql
    ALTER SCHEMA my_schema RENAME TO new_schema_name;
    ```
* **`ALTER TABLE`:** Modifies a table.
    ```sql
    -- Add column
    ALTER TABLE customers ADD COLUMN phone_number VARCHAR(20);
    -- Drop column
    ALTER TABLE customers DROP COLUMN phone_number;
    -- Add NOT NULL constraint
    ALTER TABLE customers ALTER COLUMN last_name SET NOT NULL;
    -- Add UNIQUE constraint
    ALTER TABLE customers ADD CONSTRAINT unique_email UNIQUE (email);
    ```
* **`DROP DATABASE`:** Deletes a database.
    ```sql
    DROP DATABASE new_database_name;
    ```
* **`DROP SCHEMA`:** Deletes a schema.
    ```sql
    DROP SCHEMA new_schema_name CASCADE;
    ```
* **`DROP TABLE`:** Deletes a table.
    ```sql
    DROP TABLE customers;
    ```

### 4.2 Data Manipulation Language (DML)
Used to interact with the data stored in tables.

* **`INSERT INTO`:** Adds new rows to a table.
    ```sql
    INSERT INTO customers (first_name, last_name, email)
    VALUES ('John', 'Doe', 'john.doe@example.com');
    ```
* **`SELECT`:** Retrieves data from tables.
    ```sql
    SELECT * FROM customers;
    SELECT first_name, last_name FROM customers;
    SELECT first_name AS "Given Name" FROM customers;
    ```
* **`WHERE` clause:** Filters rows based on conditions.
    ```sql
    SELECT * FROM customers WHERE first_name = 'John';
    SELECT * FROM customers WHERE registration_date > '2025-04-10';
    SELECT * FROM customers WHERE email LIKE '%example.com';
    SELECT * FROM customers WHERE first_name ILIKE 'jane%';
    SELECT * FROM customers WHERE customer_id IN (1, 3, 5);
    SELECT * FROM customers WHERE registration_date BETWEEN '2025-04-01' AND '2025-04-15';
    SELECT * FROM customers WHERE last_name IS NULL;
    ```
* **`ORDER BY` clause:** Sorts the result set.
    ```sql
    SELECT * FROM customers ORDER BY last_name ASC, first_name DESC;
    ```
* **`LIMIT` and `OFFSET`:** Implements pagination.
    ```sql
    SELECT * FROM customers LIMIT 10;
    SELECT * FROM customers LIMIT 5 OFFSET 10;
    ```
* **`UPDATE`:** Modifies existing rows.
    ```sql
    UPDATE customers SET email = 'new.email@example.com' WHERE customer_id = 1;
    ```
* **`DELETE`:** Removes rows from a table.
    ```sql
    DELETE FROM customers WHERE customer_id = 5;
    ```

## Chapter 5: PostgreSQL Data Types

PostgreSQL offers a rich set of built-in data types.

### 5.1 Numeric Types
`INTEGER`, `BIGINT`, `SMALLINT`, `REAL`, `DOUBLE PRECISION`, `DECIMAL`, `NUMERIC`, `SERIAL`, `BIGSERIAL`, `SMALLSERIAL`.

### 5.2 Character Types
`VARCHAR(n)`, `TEXT`, `CHAR(n)`.

### 5.3 Date and Time Types
`DATE`, `TIME`, `TIMESTAMP`, `TIMESTAMPTZ`, `INTERVAL`.

### 5.4 Boolean Type
`BOOLEAN` or `BOOL`.

### 5.5 Other Common Types
`JSON`, `JSONB`, `ARRAY`, `UUID`, `BYTEA`, `INET`, `CIDR`, `GEOMETRY` (with PostGIS).

## Chapter 6: Operators

PostgreSQL supports various operators for different operations.

### 6.1 Comparison Operators
`=`, `>`, `<`, `>=`, `<=`, `<>` or `!=`.

### 6.2 Logical Operators
`AND`, `OR`, `NOT`.

### 6.3 String Operators
`||` (concatenation), `LIKE`, `ILIKE`, `NOT LIKE`, `NOT ILIKE`, regular expression operators (`~`, `~*`, `!~`, `!~*`).

### 6.4 Arithmetic Operators
`+`, `-`, `*`, `/`, `%`.

### 6.5 Set Operators
`UNION`, `UNION ALL`, `INTERSECT`, `EXCEPT`.

## Chapter 7: Functions

PostgreSQL provides a wide array of built-in functions.

### 7.1 Aggregate Functions
`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`.

### 7.2 String Functions
`LOWER`, `UPPER`, `TRIM`, `SUBSTRING`, `LENGTH`, `CONCAT`.

### 7.3 Date/Time Functions
`NOW`, `CURRENT_DATE`, `CURRENT_TIME`, `EXTRACT`, `AGE`.

### 7.4 Numeric Functions
`ABS`, `ROUND`, `CEIL`, `FLOOR`.

**(Further chapters will cover Joins, Grouping, Constraints, Indexes, Transactions, Views, Roles, and Backup/Restore in subsequent lessons.)**
