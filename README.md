# SQL Basics Code Examples

This GitHub repo contains SQL code examples that explain different aspects of SQL. Each example is contained in a separate SQL file.

## Create a Database

```create_database.sql
-- Create a new database called my_database
CREATE DATABASE my_database;
```

## Create a Table

```create_table.sql
-- Create a new table called my_table with two columns: id and name
CREATE TABLE my_table (
id INT PRIMARY KEY,
name VARCHAR(50)
);
```


## Insert Data

```insert_data.sql
-- Insert data into the my_table table
INSERT INTO my_table (id, name)
VALUES (1, 'John'), (2, 'Jane'), (3, 'Bob');
```

## Select Data

```select_data.sql
-- Select all data from the my_table table
SELECT * FROM my_table;
```

## WHERE Clause

```where_clause.sql
-- Select data from the my_table table where the name is 'John'
SELECT * FROM my_table WHERE name = 'John';
```

## ORDER BY Clause

```order_by.sql
-- Select data from the [my_table] table and order it by the [name] column in ASC/DESC order
SELECT * FROM my_table ORDER BY name ASC;
SELECT * FROM my_table ORDER BY name DESC;
```

## GROUP BY Clause
#### We can use the GROUP BY clause to group the orders by customer and calculate the total amount spent by each customer.

```
| order_id | customer_id | order_date  | total_amount |
| -------- | ----------- | ----------- | ------------ |
| 1        | 1           | 2022-01-01  | 100.00       |
| 2        | 1           | 2022-01-03  | 50.00        |
| 3        | 2           | 2022-01-05  | 75.00        |
| 4        | 2           | 2022-01-07  | 200.00       |
| 5        | 3           | 2022-01-10  | 150.00       |
```

```group_by.sql
-- In this query, we are grouping the orders by customer_id, and then using the aggregate function SUM to calculate the total amount spent by each customer.

SELECT customer_id, SUM(total_amount) as total_spent
FROM orders
GROUP BY customer_id;
```

#### The resulting table would look like this:

```
| customer_id | total_spent |
| ----------- | ----------- |
| 1           | 150.00      |
| 2           | 275.00      |
| 3           | 150.00      |
```

## JOIN Tables

```join.sql
-- Join the my_table and another_table tables on the id column
SELECT *
FROM my_table
JOIN another_table ON my_table.id = another_table.id;
```

## Sub-queries

```subquery.sql
-- Select data from the my_table table where the id is in a subquery
SELECT * FROM my_table WHERE id IN (SELECT id FROM another_table);
```

## Views

```views.sql
-- Create a view called my_view that selects data from the my_table table where the name is 'John'
CREATE VIEW my_view AS
SELECT * FROM my_table WHERE name = 'John';
```

## Stored Procedures

```stored_procedures.sql
-- Create a stored procedure called my_proc that inserts data into the my_table table
CREATE PROCEDURE my_proc
@id INT,
@name VARCHAR(50)
AS
BEGIN
INSERT INTO my_table (id, name) VALUES (@id, @name);
END;
```

## Transactions

```transactions.sql
-- Begin a transaction, insert data into the my_table table, and commit the transaction
BEGIN TRANSACTION;
INSERT INTO my_table (id, name) VALUES (4, 'Sarah');
COMMIT TRANSACTION;
```

#### I hope you find these examples helpful. Let me know if you have any questions or need to add more codes.
