# Amazon E-commerce SQL Project

![Project Banner Placeholder](https://github.com/najirh/Amazon--SQL-Project-B01/blob/main/Amazon.jpg)

Welcome to my SQL project, where I analyze real-time data from **Amazon.com**! This project uses a dataset of **20,000+ sales records** and additional tables for payments, products, and shipping data to explore and analyze e-commerce transactions, product sales, and customer interactions. The project aims to solve business problems through SQL queries, helping Amazon make informed decisions.

## Table of Contents
- [Introduction](#introduction)
- [Project Structure](#project-structure)
- [Database Schema](#database-schema)
- [Business Problems](#business-problems)
- [SQL Queries & Analysis](#sql-queries--analysis)
- [Getting Started](#getting-started)
- [Questions & Feedback](#questions--feedback)
- [Contact Me](#contact-me)

---

## Introduction

This project demonstrates essential SQL skills by analyzing e-commerce data from **Amazon**, focusing on sales, payments, products, and customer data. Through SQL, we answer critical business questions, uncover trends, and derive actionable insights that help improve business strategies and customer experiences. The project covers different SQL techniques including **Joins**, **Group By**, **Aggregations**, and **Date Functions**.

## Project Structure

1. **SQL Scripts**: Contains code to create the database schema and write queries for analysis.
2. **Dataset**: Real-time data representing e-commerce transactions, product details, customer information, and shipping status.
3. **Analysis**: SQL queries crafted to solve business problems, each focusing on understanding e-commerce sales and performance.

---

## Database Schema

Here’s an overview of the database structure:

### 1. **Customers Table**
- **customer_id**: Unique identifier for each customer
- **customer_name**: Name of the customer
- **state**: Location (state) of the customer

### 2. **Products Table**
- **product_id**: Unique identifier for each product
- **product_name**: Name of the product
- **price**: Price of the product
- **cogs**: Cost of goods sold
- **category**: Category of the product
- **brand**: Brand name of the product

### 3. **Sales Table**
- **order_id**: Unique order identifier
- **order_date**: Date the order was placed
- **customer_id**: Linked to the `customers` table
- **order_status**: Status of the order (e.g., Completed, Cancelled)
- **product_id**: Linked to the `products` table
- **quantity**: Quantity of products sold
- **price_per_unit**: Price per unit of the product

### 4. **Payments Table**
- **payment_id**: Unique payment identifier
- **order_id**: Linked to the `sales` table
- **payment_date**: Date the payment was made
- **payment_status**: Status of the payment (e.g., Payment Successed, Payment Failed)

### 5. **Shippings Table**
- **shipping_id**: Unique shipping identifier
- **order_id**: Linked to the `sales` table
- **shipping_date**: Date the order was shipped
- **return_date**: Date the order was returned (if applicable)
- **shipping_providers**: Shipping provider (e.g., Ekart, Bluedart)
- **delivery_status**: Status of delivery (e.g., Delivered, Returned)

## Business Problems

The following queries were created to solve specific business questions. Each query is designed to provide insights based on sales, payments, products, and customer data.

### Easy 
1. `Retrieve a list of all customers with the corresponding product names they ordered.`
```sql
select 
	customers.customer_name,
	products.product_name
from customers
Inner JOIN sales
ON sales.customer_id = customers.customer_id
Inner JOIN products
ON sales.product_id = products.product_id
Order By 1 ASC;
```
2. `List all products and show the details of customers who have placed orders for them. Include products that have no orders.`
```sql
select 
	products.product_name as Product,
	customers.customer_name as Customer
from products
LEFT JOIN sales
ON products.product_id = sales.product_id
LEFT JOIN customers
ON customers.customer_id = sales.customer_id
GROUP BY 1, 2
ORDER BY 1 ASC;
```
3. `List all orders and their shipping status. Include orders that do not have any shipping records.`
```sql
select 
	sales.order_id,
	sales.order_date,
	sales.order_status,
	shippings.shipping_date,
	shippings.shipping_providers,
	shippings.delivery_status
from sales
LEFT JOIN shippings
ON sales.order_id = shippings.order_id;
```

4. `Retrieve all products, including those with no orders, along with their price.`
```sql
select 
	products.product_name,
	products.price,
	sales.price_per_unit
from sales
RIGHT JOIN products
ON sales.product_id = products.product_id;
```
5. `Get a list of all customers who have placed orders, including those with no payment records.`
```sql
select 
	Distinct(customers.customer_id),
	customers.customer_name,
	sales.order_id,
	payments.payment_id
from customers
LEFT JOIN sales
ON customers.customer_id = sales.customer_id
LEFT JOIN payments
ON payments.order_id = sales.order_id;
```
6. `Find the total number of completed orders made by customers from the state 'Delhi'.`
```sql
select 
	COUNT(*) as total_number_of_completed_orders
from customers
INNER JOIN sales
ON customers.customer_id = sales.customer_id
Where customers.state = 'Delhi' and sales.order_status = 'Completed';
```
7. `Retrieve a list of products ordered by customers from the state 'Karnataka' with price greater than 10,000.`
```sql
select 
	products.product_name 
FROM customers
INNER JOIN sales
ON customers.customer_id = sales.customer_id
INNER JOIN products
ON sales.product_id = products.product_id
Where customers.state = 'Karnataka' and products.price > 10000;
```
8. `List all customers who have placed orders where the product category is 'Accessories' and the order status is 'Completed'.`
```sql
select
	DISTINCT(customers.customer_id),
	customers.customer_name
FROM customers
INNER JOIN sales
ON customers.customer_id = sales.customer_id
INNER JOIN products
ON sales.product_id = products.product_id
Where sales.order_status = 'Completed' and products.category = 'Accessories'
ORDER BY 1 ASC;
```
9. `Show the order details of customers who have paid for their orders, excluding those who have cancelled their orders.'
```sql
select
	*
FROM customers
INNER JOIN sales
ON customers.customer_id = sales.customer_id
INNER JOIN payments
ON payments.order_id = sales.order_id
WHERE sales.order_status <> 'Canceled' and payments.payment_status = 'Payment Successed';
```
10. `Retrieve products ordered by customers who are in the 'Gujarat' state and whose total order price is greater than 15,000`
```sql
select
	customers.customer_id,
	products.product_name,
	sales.quantity,
	sales.price_per_unit,
	customers.state
FROM customers
INNER JOIN sales
ON customers.customer_id = sales.customer_id
INNER JOIN products
ON sales.product_id = products.product_id
Where customers.state = 'Gujarat' and (sales.quantity * sales.price_per_unit) > 15000;
```
   
### Medium to Hard
1. `Add your questions here`
2. `Add your questions here`
3. `Add your questions here`
4. `Add your questions here`
5. `Add your questions here`
   
---

## SQL Queries & Analysis

The `queries.sql` file contains all SQL queries developed for this project. Each query corresponds to a business problem and demonstrates skills in SQL syntax, data filtering, aggregation, grouping, and ordering.

---

## Getting Started

### Prerequisites
- PostgreSQL (or any SQL-compatible database)
- Basic understanding of SQL

### Steps
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/Amazon-sql-project.git
   ```
2. **Set Up the Database**:
   - Run the `schema.sql` script to set up tables and insert sample data.

3. **Run Queries**:
   - Execute each query in `queries.sql` to explore and analyze the data.

---

## Questions & Feedback

Feel free to add your questions and code snippets below and submit them as issues for further feedback!

**Example Questions**:
1. **Question**: How can I filter orders placed in the last 6 months?
   **Code Snippet**:
   ```sql
   SELECT * FROM sales
   WHERE order_date >= CURRENT_DATE - INTERVAL '6 months';
   ```

---

## Contact Me

📄 **[Resume](#)**  
📧 **[Email](mailto:your.email@example.com)**  
📞 **Phone**: +123-456-7890  

---

## ERD (Entity-Relationship Diagram)

## Notice:
All customer names and data used in this project are computer-generated using AI and random
functions. They do not represent real data associated with Amazon or any other entity. This
project is solely for learning and educational purposes, and any resemblance to actual persons,
businesses, or events is purely coincidental.

![ERD Placeholder](https://github.com/najirh/Amazon--SQL-Project-B01/blob/main/Amazon%20Project%20Schemas.png)
