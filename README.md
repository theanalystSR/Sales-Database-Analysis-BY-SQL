Sales Database Analysis
This project demonstrates how to analyze sales data using SQL. The goal is to extract and transform data from multiple related tables, perform detailed analysis of product sales, and rank top-performing products using SQL window functions.

Tools & Technologies
SQL (JOINs, GROUP BY, HAVING, Window Functions)
Database: Simulated database schema with sales, products, and customers tables.
Project Description
The project focuses on:

Extracting Data: Combining data from multiple related tables using SQL JOINs.
Data Transformation: Aggregating sales data using SQL GROUP BY and HAVING clauses.
Ranking Products: Using SQL Window Functions (RANK() and ROW_NUMBER()) to rank top-selling products.
Visualization: Generating insights on the highest-performing products for optimizing sales and inventory management.
Database Schema
The project simulates a sales database with three main tables:

Products: Contains product information (e.g., product name, category).
Customers: Stores customer information (e.g., customer name, region).
Sales: Stores sales transactions (e.g., product ID, customer ID, quantity sold, sale price).
SQL Schema:
sql
Copy code
-- Create the tables
CREATE TABLE Products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(100)
);

CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100),
    region VARCHAR(100)
);

CREATE TABLE Sales (
    sale_id INT PRIMARY KEY,
    product_id INT,
    customer_id INT,
    sale_date DATE,
    quantity INT,
    price DECIMAL(10, 2),
    FOREIGN KEY (product_id) REFERENCES Products(product_id),
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
);
SQL Queries
1. Extracting Data with JOINs:
sql
Copy code
SELECT s.sale_id, p.product_name, c.customer_name, s.sale_date, s.quantity, s.price
FROM Sales s
JOIN Products p ON s.product_id = p.product_id
JOIN Customers c ON s.customer_id = c.customer_id;
2. Aggregating Data with GROUP BY:
sql
Copy code
SELECT p.product_name, SUM(s.quantity) AS total_quantity, SUM(s.quantity * s.price) AS total_sales
FROM Sales s
JOIN Products p ON s.product_id = p.product_id
GROUP BY p.product_name
HAVING SUM(s.quantity) > 1;
3. Ranking Products using Window Functions:
sql
Copy code
SELECT p.product_name, 
       SUM(s.quantity * s.price) AS total_sales,
       RANK() OVER (ORDER BY SUM(s.quantity * s.price) DESC) AS product_rank
FROM Sales s
JOIN Products p ON s.product_id = p.product_id
GROUP BY p.product_name;
Example Output
After running the query, the ranked products data looks like:

Product Name	Total Sales ($)	Product Rank
Laptop	5000	1
Phone	2500	2
Monitor	300	3
Visualization
Here’s a bar chart representing the Product Ranking by Total Sales:


Results
Top Product: The highest-performing product is Laptop with total sales of $5000.
Sales Insights: The ranking helps the sales team identify top-selling products and optimize inventory management.
How to Run the Project
Set up a database with the provided schema.
Insert sample data into the Products, Customers, and Sales tables.
Run the SQL queries to analyze the sales data.
Generate visualizations (if needed) using tools like Excel, Tableau, or Python.
License
This project is licensed under the MIT License - see the LICENSE file for details.

