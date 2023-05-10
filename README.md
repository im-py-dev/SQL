# SQL Basics Code Examples

This GitHub repo contains SQL code examples that explain different aspects of SQL. Each example is contained in a separate SQL file.

## Create a Database

```sql
-- Create a new database called my_database
CREATE DATABASE my_database;
```
__________
## Create a Table

```sql
-- Create a new table called my_table with two columns: id and name
CREATE TABLE my_table (
id INT PRIMARY KEY,
name VARCHAR(50)
);
```

__________
## Insert Data

```sql
-- Insert data into the my_table table
INSERT INTO my_table (id, name)
VALUES (1, 'John'), (2, 'Jane'), (3, 'Bob');
```
__________
## Updating data
###### To update existing data in your table, use the UPDATE command followed by the name of your table, the column you want to update, and the new value:

```sql
UPDATE mytable
SET age = 35
WHERE name = 'John';
```
__________
## Deleting data:
###### To delete data from your table, use the DELETE FROM command followed by the name of your table and a condition that specifies which rows to delete:

```sql
DELETE FROM mytable
WHERE age > 30;
```
__________
## Select Data

```sql
-- Select all data from the my_table table
SELECT * FROM my_table;
```
__________
## WHERE Clause

```sql
-- Select data from the my_table table where the name is 'John'
SELECT * FROM my_table WHERE name = 'John';
```
__________
## ORDER BY Clause

```sql
-- Select data from the [my_table] table and order it by the [name] column in ASC/DESC order
SELECT * FROM my_table ORDER BY name ASC;
SELECT * FROM my_table ORDER BY name DESC;
```
__________
## Aggregating data
##### To perform calculations on your data, use aggregate functions like `COUNT`, `SUM`, `AVG`, `MAX`, and `MIN`.
##### You can also use the GROUP BY clause to group your data by one or more columns.
##### We can use the GROUP BY clause to group the orders by customer and calculate the total amount spent by each customer.


```
| order_id | customer_id | order_date  | total_amount |
| -------- | ----------- | ----------- | ------------ |
| 1        | 1           | 2022-01-01  | 100.00       |
| 2        | 1           | 2022-01-03  | 50.00        |
| 3        | 2           | 2022-01-05  | 75.00        |
| 4        | 2           | 2022-01-07  | 200.00       |
| 5        | 3           | 2022-01-10  | 150.00       |
```

```sql
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
__________
## JOIN Tables

#### Let's consider two tables, "orders" and "customers", that contain information about orders placed by customers:

```
Orders Table:

| order_id | customer_id | order_date  | total_amount |
| -------- | ----------- | ----------- | ------------ |
| 1        | 1           | 2022-01-01  | 100.00       |
| 2        | 1           | 2022-01-03  | 50.00        |
| 3        | 2           | 2022-01-05  | 75.00        |
| 4        | 2           | 2022-01-07  | 200.00       |
| 5        | 3           | 2022-01-10  | 150.00       |

Customers Table:

| customer_id | first_name | last_name  | phone_number  |
| ----------- | ---------- | ---------- | ------------- |
| 1           | John       | Doe        | 555-555-1234  |
| 2           | Jane       | Smith      | 555-555-5678  |
| 3           | Bob        | Johnson    | 555-555-9012  |
```

#### We can join these two tables using the "customer_id" column, which is present in both tables:

```sql
SELECT orders.order_id, customers.first_name, customers.last_name, orders.order_date, orders.total_amount
FROM orders
JOIN customers ON orders.customer_id = customers.customer_id;
```

#### This query will return a result set that includes the order details along with the corresponding customer information:

```
| order_id | first_name | last_name | order_date  | total_amount |
| -------- | ---------- | --------- | ----------- | ------------ |
| 1        | John       | Doe       | 2022-01-01  | 100.00       |
| 2        | John       | Doe       | 2022-01-03  | 50.00        |
| 3        | Jane       | Smith     | 2022-01-05  | 75.00        |
| 4        | Jane       | Smith     | 2022-01-07  | 200.00       |
| 5        | Bob        | Johnson   | 2022-01-10  | 150.00       |
```

#### As you can see, the result set includes the order details and the corresponding customer details based on the "customer_id" column that is present in both tables.

__________
## Sub-queries

```sql
-- Select data from the my_table table where the id is in a subquery
SELECT * FROM my_table WHERE id IN (SELECT id FROM another_table);
```
__________
## Views

##### Here are some key points to understand about views:

* A view is defined by a SELECT statement that specifies the columns and rows to include in the view.
* Once a view is created, it can be used like a regular table in SQL queries, including SELECT, INSERT, UPDATE, and DELETE statements.
* Views are often used to simplify complex queries by providing a simplified and focused view of the data.
* Views can also be used to restrict access to certain columns or rows of a table by granting access to the view instead of the underlying table.
* Views can be used to aggregate data from multiple tables into a single view, making it easier to work with the data in reporting and analysis.
* Here's an example of creating a view in SQL:

```sql
CREATE VIEW customer_orders AS
SELECT customers.first_name, customers.last_name, orders.order_date, orders.total_amount
FROM orders
JOIN customers ON orders.customer_id = customers.customer_id;
```
##### This SQL statement creates a view called "customer_orders" that includes columns from the "orders" and "customers" tables.
##### The view selects the "first_name", "last_name", "order_date", and "total_amount" columns from the "orders" and "customers" tables, based on a JOIN between the two tables on the "customer_id" column.
##### Once the view is created, it can be used in SQL queries just like any other table.
##### For example, to retrieve all orders for a specific customer, you could use the following SQL statement:

```sql
SELECT * FROM customer_orders WHERE first_name = 'John' AND last_name = 'Doe';
This query retrieves all orders for the customer named John Doe, based on the "customer_orders" view that was created earlier.
```

##### In summary, views are a powerful tool in SQL that can be used to simplify complex queries, present data in a different way, and restrict access to sensitive data.
They can be created using a SELECT statement and can be used like any other table in SQL queries.

* #### [Q] what if we insert data after create the view, should the view be able to see new updates?
* #### [A] Yes, the view will be able to see new updates to the underlying tables after it is created. Views are based on SELECT statements, so the data in the view is determined by the SELECT statement used to create it. If new data is added to the underlying tables, it will be reflected in the view as long as the SELECT statement in the view definition includes the new data.

__________
## Stored Procedures

##### A stored procedure is a named block of code that is stored in a database and can be called multiple times with different input parameters. Stored procedures can be used to encapsulate complex SQL statements, improve performance by reducing network traffic and allowing code to be precompiled, and improve security by allowing controlled access to the database.

###### Here's an example of a simple stored procedure in SQL:

```sql
CREATE PROCEDURE get_customer_orders
    @customer_id INT
AS
BEGIN
    SELECT * FROM orders WHERE customer_id = @customer_id;
END
```

##### In this example, we're creating a stored procedure called get_customer_orders that takes an input parameter @customer_id and returns all orders for that customer.

###### To call this stored procedure, we would use the following syntax:

```sql
EXEC get_customer_orders @customer_id = 1;
```
##### In this example, we're calling the get_customer_orders stored procedure and passing in a value of 1 for the @customer_id parameter.

##### Here's a real-world scenario where a stored procedure might be useful:

##### Let's say you're working on an e-commerce website that sells products to customers around the world. You have a database table called orders that contains information about all orders placed by customers. You need to write a report that shows the total revenue for each country where you have customers.

##### Instead of writing a complex SQL query every time you need to generate this report, you could create a stored procedure that encapsulates the SQL logic and takes a country parameter as input. You could then call this stored procedure multiple times with different country parameters to generate the report for each country.

###### In summary, stored procedures in SQL are a powerful tool for encapsulating complex SQL logic, improving performance and security, and simplifying common tasks. They can be called multiple times with different input parameters, making them a versatile solution for many database-related challenges.
__________
## Transactions

##### In SQL, a transaction is a set of database operations that are executed as a single unit of work. Transactions ensure that all operations within the transaction are either committed to the database together or rolled back as a single unit, ensuring data consistency and integrity.

###### Here's an example of a simple transaction in SQL:

```sql
BEGIN TRANSACTION;

UPDATE accounts SET balance = balance - 100 WHERE account_id = 1;
UPDATE accounts SET balance = balance + 100 WHERE account_id = 2;

COMMIT TRANSACTION;
```
##### In this example, we're beginning a transaction, then updating the balance of two bank accounts (subtracting 100 from account 1 and adding 100 to account 2), and finally committing the transaction. If any errors occur during the transaction, the changes made by the updates will be rolled back.

###### Here's a real-world scenario where transactions might be useful:

##### Let's say you're working on an e-commerce website that sells products to customers. You have a database table called orders that contains information about all orders placed by customers, and a table called inventory that contains information about the available stock of each product.

##### When a customer places an order, you need to update the orders table to record the order, and also update the inventory table to reflect the change in stock. However, if the inventory is insufficient to fulfill the order, you want to roll back the entire transaction and not update either table.

##### In this scenario, you could use a transaction to ensure that the updates to both tables are committed together or rolled back together if an error occurs. Here's an example of a transaction that updates both tables:

```sql
BEGIN TRANSACTION;

INSERT INTO orders (customer_id, product_id, quantity, total_price)
VALUES (1, 123, 2, 100);

UPDATE inventory SET stock = stock - 2 WHERE product_id = 123;

COMMIT TRANSACTION;
```

In this example, we're beginning a transaction, inserting a new order into the orders table, updating the inventory table to reflect the change in stock, and finally committing the transaction. If there's not enough stock to fulfill the order, the transaction will be rolled back and no changes will be made to either table.

In summary, transactions in SQL are a powerful tool for ensuring data consistency and integrity, especially in complex scenarios where multiple tables need to be updated together or rolled back together. They help ensure that all operations within the transaction are either committed to the database together or rolled back as a single unit, avoiding errors and maintaining data integrity.
__________

#### I hope you find these examples helpful. Let me know if you have any questions or need to add more codes.
