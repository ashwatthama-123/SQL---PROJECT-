# Retail Sales Analysis SQL Project

## Project Overview

**Project Title**: Retail Sales Analysis  
**Database**: `SQLPROJECT`

This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze retail sales data. The project involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries.

## Objectives

1. **Set up a retail sales database**: Create and populate a SQLPROJECT database with the provided sales data.
2. **Data Cleaning**: Identify and remove any records with missing or null values.
3. **Exploratory Data Analysis (EDA)**: Perform basic exploratory data analysis to understand the dataset.
4. **Business Analysis**: Use SQL to answer specific business questions and derive insights from the sales data.

## Project Structure

### 1. Database Setup

- **Database Creation**: The project starts by creating a database named `SQLPROJECT`.
- **Table Creation**: A table named `RETAIL_SALES` is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.

```sql
CREATE DATABASE SQLPROJECT;

CREATE TABLE RETAIL_SALES
(
CREATE TABLE RETAIL_SALES (
TRANSACTIONS_ID INT,
SALE_DATE DATE,
SALE_TIME TIME,
CUSTOMER_ID INT,
GENDER VARCHAR (10),
AGE INT,
CATEGORY VARCHAR (50), 
QUANTIY INT,
PRICE_PER_UNIT FLOAT,
COGS FLOAT,
TOTAL_SALE FLOAT);
```

### 2. Data Exploration & Cleaning

- **Record Count**: Determine the total number of records in the dataset.
- **Customer Count**: Find out how many unique customers are in the dataset.
- **Category Count**: Identify all unique product categories in the dataset.
- **Null Value Check**: Check for any null values in the dataset and delete records with missing data.

```sql
SELECT COUNT(*) FROM RETAIL_SALES;

There are 2000 thousand records in dataset

SELECT * FROM RETAIL_SALES
WHERE
TRANSACTIONS_ID IS NULL OR SALE_DATE IS NULL OR SALE_TIME IS NULL OR
CUSTOMER_ID IS NULL OR GENDER IS NULL OR CATEGORY IS NULL OR QUANTIY IS NULL OR 
PRICE_PER_UNIT IS NULL OR COGS IS NULL OR TOTAL_SALE IS NULL;

DELETE FROM RETAIL_SALES
WHERE
TRANSACTIONS_ID IS NULL OR SALE_DATE IS NULL OR SALE_TIME IS NULL OR
CUSTOMER_ID IS NULL OR GENDER IS NULL OR CATEGORY IS NULL OR QUANTIY IS NULL OR 
PRICE_PER_UNIT IS NULL OR COGS IS NULL OR TOTAL_SALE IS NULL;

After cleaninig NULL values the dataset is now 1997.

```

### 3. Data Analysis & Findings

The following SQL queries were developed to answer specific business questions:

1. **Write a SQL query to retrieve all columns for sales made on '2022-11-05**:
```sql
SELECT * FROM RETAIL_SALES
WHERE
SALE_DATE = '2022-11-05';
```

2. **Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022**:
```sql
SELECT * FROM RETAIL_SALES
WHERE
CATEGORY = 'CLOTHING' AND SALE_DATE = '2022-11' AND QUANTIY >= 4 
```

3. **Write a query to calculate the total sales (total_sale) for each category.**:
```sql
SELECT CATEGORY, SUM(TOTAL_SALE)
AS NET_SALE, COUNT (*) AS TOTALORDERS
FROM RETAIL_SALES GROUP BY CATEGORY
```

4. **Write a query to find the average age of customers who purchased items from the 'Beauty' category.**:
```sql
SELECT AVG(AGE)
AS AVG_AGE FROM RETAIL_SALES
WHERE CATEGORY = 'BEAUTY'
```

5. **Write a SQL query to find all transactions where the total_sale is greater than 1000.**:
```sql
SELECT * FROM RETAIL_SALES
WHERE TOTAL_SALE > '1000';
```

6. **Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.**:
```sql
SELECT CATEGORY, GENDER, COUNT (*)
AS TOTAL_TRANS FROM RETAIL_SALES
GROUP BY CATEGORY, GENDER ORDER BY 1
```

7. **Write a SQL query to find the top 5 customers based on the highest total sales**:
```sql
SELECT TOP 5 CUSTOMER_ID,
SUM (TOTAL_SALE) AS TOTAL_SALES
FROM RETAIL_SALES GROUP BY CUSTOMER_ID
ORDER BY 2 DESC 
```

8. **Write a SQL query to find the number of unique customers who purchased items from each category.**:
```sql
SELECT CATEGORY, COUNT(DISTINCT CUSTOMER_ID)
AS CNT_UNIQUE_CS
FROM RETAIL_SALES GROUP BY CATEGORY 
```

9. **Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17) **:
```sql
WITH HOURLY_SALE AS
(SELECT *, CASE WHEN EXTRACT(HOUR FROM SALE_TIME)
< 12 THEN'MORNING' WHEN EXTRACT (HOUR FROM SALE_TIME)
BETWEEN 12 AND 17 THEN 'AFTERNOON'
ELSE 'EVENING' END AS SHIFT FROM RETAIL_SALES)
SELECT SHIFT, COUNT(*) AS TOTAL_ORDERS
FROM HOURLY_SALE GROUP BY SHIFT 
```

10. **A SQL query to calculate the average sale for each month find out the best selling month in each year**:
```sql
SELECT YEAR, MONTH, AVG_SALE
FROM (SELECT EXTRACT(YEAR FROM SALE_DATE) AS YEAR,
EXTRACT (MONTH FROM SALE_DATE) AS MONTH, AVG(TOTAL_SALE) AS AVG_SALE,
RANK() OVER(PARTITION BY EXTRACT(YEAR FROM SALE_DATE)
ORDER BY AVG(TOTAL_SALE) DESC)
AS RANK FROM RETAIL_SALES GROUP BY SALE_DATE, SALE_TIME)
AS T1 WHERE RANK = 1
  
```

## Reports

- **Sales Summary**: A detailed report summarizing total sales, customer demographics, and category performance.
- **Trend Analysis**: Insights into sales trends across different months and shifts.
- **Customer Insights**: Reports on top customers and unique customer counts per category.

## Conclusion

This project serves as a comprehensive introduction to SQL for data analysts, covering database setup, data cleaning, exploratory data analysis, and business-driven SQL queries. The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.

                                                                       
*END OF PROJECT* 

 **LinkedIn**: [Connect with me](https://www.linkedin.com/in/vishal-porla-ba580a340/)

  *Thankyou for your VISIT*

