# SQL Cheatsheet for Data Science and Data Engineering

This cheatsheet provides a quick reference for essential SQL commands and concepts.  It goes beyond generic commands to include essential topics for data scientists and engineers, such as window functions and other advanced concepts often overlooked in basic cheatsheets.

## Table of Contents

1. [Relational Database Model](#relational-database-model)
2. [SQL Query Commands](#sql-query-commands)
   - [Basic SELECT](#basic-select)
   - [DISTINCT](#distinct)
   - [GROUP BY](#group-by)
3. [Handling Null Values](#handling-null-values)
   - [IS NULL](#is-null)
   - [COALESCE](#coalesce)
   - [IFNULL](#ifnull)
4. [Joins](#joins)
   - [INNER JOIN](#inner-join)
   - [LEFT JOIN](#left-join)
   - [FULL OUTER JOIN](#full-outer-join)
5. [Key Constraints](#key-constraints)
   - [Primary Key](#primary-key)
   - [Foreign Key](#foreign-key)
   - [Unique Constraint](#unique-constraint)
6. [Working with Subqueries](#working-with-subqueries)
   - [Subquery in SELECT](#subquery-in-select)
   - [Subquery in WHERE](#subquery-in-where)
   - [Correlated Subquery](#correlated-subquery)
7. [Creating Tables and Databases](#creating-tables-and-databases)
   - [CREATE DATABASE](#create-database)
   - [CREATE TABLE](#create-table)
   - [ALTER TABLE](#alter-table)
   - [DROP TABLE](#drop-table)
8. [Aggregations](#aggregations)
9. [Window Functions](#window-functions)
   - [RANK()](#rank)
   - [ROW_NUMBER()](#row_number)
   - [DENSE_RANK()](#dense_rank)
10. [Common Table Expressions (CTEs)](#common-table-expressions-ctes)
11. [Data Manipulation](#data-manipulation)
    - [INSERT](#insert)
    - [UPDATE](#update)
    - [DELETE](#delete)
12. [Performance Optimization](#performance-optimization)
    - [Creating Indexes](#creating-indexes)
    - [EXPLAIN](#explain)


## Relational Database Model

The relational database model organizes data into tables with relationships between them. It's the foundation of SQL databases.

### Key concepts:

- **Tables (Relations):** Store data in rows and columns
- **Rows (Tuples):** Individual records in a table
- **Columns (Attributes):** Specific fields in a table
- **Primary Keys:** Unique identifiers for each row
- **Foreign Keys:** Links between tables
- **Normalization:** The process of organizing data to reduce redundancy



## SQL Query Commands

### Basic SELECT
Retrieves data from one or more tables.

```sql
SELECT column1, column2
FROM table_name
WHERE condition
ORDER BY column1 [ASC|DESC]
LIMIT n;
```


### DISTINCT
Removes duplicate rows from the result set.

```sql
SELECT DISTINCT column
FROM table_name;
```

### GROUP BY
Groups rows that have the same values in specified columns.

```sql
SELECT column1, COUNT(*)
FROM table_name
GROUP BY column1
HAVING COUNT(*) > 1;
```

### Handling Null Values
Null represents missing or unknown data.

#### IS NULL
```sql
SELECT column
FROM table_name
WHERE column IS NULL;
```

COALESCE
Returns the first non-null value in a list.
```sql
SELECT COALESCE(column, 'Default Value') AS column_alias
FROM table_name;
```

### IFNULL
Replaces null with a specified value.
```sql
SELECT IFNULL(column, 'Default Value') AS column_alias
FROM table_name;
```

## Joins
Combines rows from two or more tables based on a related column between them.

### INNER JOIN
Returns records that have matching values in both tables.
```sql
SELECT t1.column, t2.column
FROM table1 t1
INNER JOIN table2 t2 ON t1.id = t2.id;
```

### LEFT JOIN
Returns all records from the left table and matched records from the right table.
```sql
SELECT t1.column, t2.column
FROM table1 t1
LEFT JOIN table2 t2 ON t1.id = t2.id;
FULL OUTER JOIN
```

### FULL OUTER JOIN
```sql
SELECT t1.column, t2.column
FROM table1 t1
FULL OUTER JOIN table2 t2 ON t1.id = t2.id;
```

## Key Constraints

### Primary Key
Uniquely identifies each record in a table.

```sql
PRIMARY KEY (column_name)
```

Establishes a link between columns in two tables.
```sql
FOREIGN KEY (column_name)
REFERENCES other_table(column_name)
```

### Unique Constraint
Ensures that all values in a column are unique.
```sql
UNIQUE (column_name)
```


## Working with Subqueries
### Subquery in SELECT
A query nested inside a SELECT statement.

```sql
SELECT column1, (SELECT AVG(column2) FROM table2) AS avg_column2
FROM table1;
```

### Subquery in WHERE
A query nested inside a WHERE clause.

```sql
SELECT column1
FROM table1
WHERE column2 = (SELECT MAX(column2) FROM table2);
```

### Correlated Subquery
A subquery that references columns from the outer query.
```sql
SELECT column1
FROM table1 t1
WHERE EXISTS (SELECT 1 FROM table2 t2 WHERE t1.id = t2.id);
```

## Creating Tables and Databases
### CREATE DATABASE
Creates a new database.

```sql
CREATE DATABASE database_name;
```

### CREATE TABLE
Creates a new table.
```sql
CREATE TABLE table_name (
    column1 datatype constraints,
    column2 datatype constraints,
    ...);
```

### ALTER TABLE
Modifies an existing table.
```sql
ALTER TABLE table_name
ADD column_name datatype;
```

### DROP TABLE
Deletes an existing table.

```sql
DROP TABLE table_name;
```

## Aggregations
Perform operations like COUNT, SUM, AVG, MIN, and MAX.

```sql
SELECT COUNT(*), AVG(column), MIN(column), MAX(column)
FROM table_name;
```

## Window Functions
Perform calculations across a set of table rows related to the current row.

## ROW_NUMBER()
Assigns a unique sequential integer to rows within a partition.
```sql
SELECT column1, ROW_NUMBER() OVER (PARTITION BY column2 ORDER BY column1) AS row_num
FROM table_name;
```

## RANK()
Assigns a unique rank to each distinct row within a partition, with gaps in ranking for ties.
```sql
SELECT column1, RANK() OVER (PARTITION BY column2 ORDER BY column1) AS rank
FROM table_name;
```

## DENSE_RANK()
Assigns a unique rank to each distinct row within a partition, with no gaps in ranking for ties.
```sql
SELECT column1, DENSE_RANK() OVER (PARTITION BY column2 ORDER BY column1) AS dense_rank
FROM table_name;
```

## Common Table Expressions (CTEs)
Named temporary result sets that can be referenced within a SELECT, INSERT, UPDATE, or DELETE statement.
```sql
WITH cte_name AS (
    SELECT column1, column2
    FROM table_name
    WHERE condition
)
SELECT *
FROM cte_name
WHERE condition;
```

## Data Manipulation
### INSERT
Adds new records to a table.

```sql
INSERT INTO table_name (column1, column2)
VALUES (value1, value2);
```

### UPDATE
Modifies existing records.
```sql
UPDATE table_name
SET column1 = value1
WHERE condition;
```

### DELETE
Removes records.

```sql
DELETE FROM table_name
WHERE condition;
```

## Performance Optimization
### Creating Indexes
Improves the speed of data retrieval operations.

```sql
CREATE INDEX index_name
ON table_name (column_name);
```

## EXPLAIN
Provides information about how a query is executed.

```sql
EXPLAIN SELECT column1
FROM table_name
WHERE condition;
```
