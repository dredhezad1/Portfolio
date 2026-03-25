# Retail Sales Analysis Project

## Project Overview
This project analyzes retail sales data using **MySQL** to understand customer behavior, sales trends, and product performance. The goal is to clean, explore, and generate business insights that can support decision-making for a retail company.

**Key Objectives:**
- Load and clean sales data.
- Perform data quality checks.
- Explore trends in customer purchases, categories, and revenue.
- Identify top customers, best-selling products, and peak sales periods.
- Generate insights for business analysis.

---

## Database and Table Setup

### Create Database

```sql
CREATE DATABASE retail_sales_db;
USE retail_sales_db;
```

### Create Retail Sales Table

```sql
CREATE TABLE retail_sales (
    transactions_id INT PRIMARY KEY,
    sale_date DATE,	
    sale_time TIME,	
    customer_id INT,
    gender VARCHAR(15),
    age INT,
    category VARCHAR(20),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
```
### Data Loading

Loads data from CSV using LOAD DATA INFILE.
Empty values are converted to NULL for proper handling.

```sql
LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/Retail_Sales.csv'
INTO TABLE retail_sales
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\r\n'
IGNORE 1 ROWS
(@transactions_id, @sale_date, @sale_time, @customer_id, @gender, @age, @category, @quantity, @price_per_unit, @cogs, @total_sale)
SET
    transactions_id = @transactions_id,
    sale_date = @sale_date,
    sale_time = @sale_time,
    customer_id = @customer_id,
    gender = @gender,
    age = NULLIF(@age, ''),
    category = @category,
    quantity = NULLIF(@quantity, ''),        
    price_per_unit = NULLIF(@price_per_unit, ''),
    cogs = NULLIF(@cogs, ''),
    total_sale = NULLIF(@total_sale, '');
```

### Data Cleaning

Checks for missing values and removes incomplete rows.

```sql
DELETE FROM retail_sales
WHERE transactions_id IS NULL
   OR sale_date IS NULL
   OR sale_time IS NULL
   OR customer_id IS NULL
   OR gender IS NULL
   OR age IS NULL
   OR category IS NULL
   OR quantity IS NULL
   OR price_per_unit IS NULL
   OR cogs IS NULL
   OR total_sale IS NULL;
```

### Data Exploration

```sql
-- Total number of sales
SELECT COUNT(*) AS total_sale FROM retail_sales;

-- Total number of unique customers
SELECT COUNT(DISTINCT customer_id) AS total_customers FROM retail_sales;

-- Number of unique categories
SELECT COUNT(DISTINCT category) AS total_categories FROM retail_sales;

-- Names of unique categories
SELECT DISTINCT category FROM retail_sales;
```

### Business Analysis Queries

```sql
-- Q1: What are the sales made on '2022-11-05'?

SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';

-- Q2: Which transactions in the 'Clothing' category had a quantity greater than 4 in Nov-2022?

SELECT 
*
FROM retail_sales
WHERE category = 'Clothing'
  AND 
  sale_date >= '2022-11-01'
  AND 
  sale_date < '2022-12-01'
  AND 
  quantity >= 4;
  
  -- Q3: What are the total sales and total number of orders for each category?
  
  SELECT 
  category,
  SUM(total_sale) AS net_sale,
  COUNT(*) AS total_orders
  FROM retail_sales
  GROUP BY category;
  
  -- Q4: What is the average age of customers who purchased items from the 'Beauty' category?
  
  SELECT
      ROUND(AVG(age), 2) AS average_age
  FROM retail_sales
  WHERE category = 'Beauty';
  
  -- Q5: Which transactions had a total sale greater than 1000?
  
  SELECT *
  FROM retail_sales
  WHERE total_sale > 1000;
  
  -- Q6: How many transactions were made by each gender in each category?
  
  SELECT 
      category,
      gender,
      COUNT(*) AS total_transactions
  FROM retail_sales
  GROUP BY category, gender
  ORDER BY category;
  
-- Q7: What was the average sale for each month, and which month was the best-selling in each year?

SELECT
    year,
    month,
    average_sale
FROM
(
SELECT 
    YEAR(sale_date) AS year,
    MONTH(sale_date) AS month,
    ROUND(AVG(total_sale), 2) AS average_sale,
    RANK() OVER(PARTITION BY YEAR(sale_date) ORDER BY AVG(total_sale) DESC) AS rnk
FROM retail_sales
GROUP BY year, month
) AS t1
WHERE rnk = 1;

-- Q8: Who are the top 5 customers based on highest total sales?

SELECT 
    customer_id,
    SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;

-- Q9: How many unique customers purchased items in each category?

SELECT 
    category,
    COUNT(DISTINCT customer_id) AS unique_customers
FROM retail_sales
GROUP BY category;

-- Q10: How many orders were made in each shift (Morning < 12, Afternoon 12-17, Evening > 17)?

WITH hourly_sales
AS
(
SELECT *,
    CASE 
        WHEN HOUR(sale_time) < 12 THEN 'Morning'
        WHEN HOUR(sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
	END AS shift
FROM retail_sales
)
SELECT 
    shift,
    COUNT(*) AS total_orders
FROM hourly_saLes
GROUP BY shift;

-- Q11: What is the total revenue per month?

SELECT
    MONTH(sale_date) AS month,
    SUM(total_sale) AS total_revenue,
    COUNT(*) AS total_orders
FROM retail_sales
GROUP BY month
ORDER BY month;

-- Q12: Who are the customers with the highest single transactions?

SELECT
    customer_id,
    sale_date,
    total_sale
FROM retail_sales
ORDER BY total_sale DESC
LIMIT 5;

-- Q13: Which categories are the most profitable on average (total_sale - cogs)?

SELECT 
    category,
    ROUND(AVG(total_sale - cogs), 2) AS average_profit
FROM retail_sales
GROUP BY category
ORDER BY average_profit DESC;

-- Q14: What is the peak sales hour overall?

SELECT 
     HOUR(sale_time) AS hour,
     SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY hour
ORDER BY total_sales DESC
LIMIT 1;

-- Q15: Which categories/products are most demanded based on quantity sold?

SELECT 
    category,
    SUM(quantity) AS total_quantity_sold
FROM retail_sales
GROUP BY category
ORDER BY total_quantity_sold DESC;
```

