# Sales-Insights-Data-Analysis-Project
Sales Insights Data Analysis Project

Data Analysis Using SQL

Show all customer records:

SQL

SELECT * FROM customers;
Show the total number of customers:



SELECT count(*) FROM customers;
Show transactions for Chennai market (market code for Chennai is Mark001):



SELECT * FROM transactions WHERE market_code = 'Mark001';
Show distinct product codes that were sold in Chennai:


SELECT DISTINCT product_code FROM transactions WHERE market_code = 'Mark001';
Show transactions where currency is in US dollars:


SELECT * FROM transactions WHERE currency = "USD";
Show transactions for the year 2020 (with a join on the date table):


SELECT transactions.*, date.* 
FROM transactions 
INNER JOIN date ON transactions.order_date = date.date 
WHERE date.year = 2020;
Show total revenue for the year 2020:


SELECT SUM(transactions.sales_amount) 
FROM transactions 
INNER JOIN date ON transactions.order_date = date.date 
WHERE date.year = 2020 AND (transactions.currency = "INR\r" OR transactions.currency = "USD\r");
Show total revenue for January 2020:


SELECT SUM(transactions.sales_amount) 
FROM transactions 
INNER JOIN date ON transactions.order_date = date.date 
WHERE date.year = 2020 AND date.month_name = "January" 
AND (transactions.currency = "INR\r" OR transactions.currency = "USD\r");
Show total revenue for the year 2020 in Chennai:


SELECT SUM(transactions.sales_amount) 
FROM transactions 
INNER JOIN date ON transactions.order_date = date.date 
WHERE date.year = 2020 AND transactions.market_code = "Mark001";
Data Analysis Using Power BI
For analyzing and visualizing the sales data in Power BI, follow these steps:

Create a norm_amount column:
Use the formula below to create a new column called norm_amount, which normalizes sales amounts to INR for transactions in USD.
powerquery

= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] = 
