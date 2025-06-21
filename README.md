Thanks for the update! Here's a personalized `README.md` file you can use for your GitHub repository based on your project and learning journey:

---

# 🛍️ Retail Sales Analysis – SQL Project

**Level**: Beginner
**Database File**: `retail_sales.csv`
**SQL Queries File**: `sales_sqlquery.sql`

## 📌 Project Overview

This project is a beginner-friendly SQL analysis of retail sales data. It was completed as part of my learning journey in data analytics. The goal was to explore, clean, and analyze sales data using SQL, and to answer common business questions through structured queries.

---

## 🎯 Objectives

* ✅ Import and structure retail sales data
* ✅ Clean the data by removing null/missing values
* ✅ Perform Exploratory Data Analysis (EDA)
* ✅ Answer business questions using SQL
* ✅ Practice SQL concepts like aggregation, filtering, grouping, and window functions

---

## 🗂️ Dataset Description

The dataset (`retail_sales.csv`) includes the following fields:

* `transactions_id` – Unique ID for each transaction
* `sale_date` – Date of sale
* `sale_time` – Time of sale
* `customer_id` – Customer identifier
* `gender` – Customer gender
* `age` – Customer age
* `category` – Product category
* `quantity` – Number of items sold
* `price_per_unit` – Selling price per unit
* `cogs` – Cost of goods sold
* `total_sale` – Total revenue from the transaction

---

## 🧹 Data Cleaning Steps

Executed the following queries to clean the data:

* Counted total records and distinct customers
* Identified nulls in important columns
* Removed rows with any missing critical data

```sql
DELETE FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;
```

---

## 📊 SQL Analysis Performed

You’ll find all queries in the `sales_sqlquery.sql` file. Key analyses include:

### ✅ Total Sales on a Specific Date

```sql
SELECT * FROM retail_sales WHERE sale_date = '2022-11-05';
```

### ✅ High Quantity Clothing Purchases in Nov-2022

```sql
SELECT * 
FROM retail_sales
WHERE category = 'Clothing' 
  AND DATE_FORMAT(sale_date, '%Y-%m') = '2022-11' 
  AND quantity >= 4;
```

### ✅ Total Sales by Category

```sql
SELECT category, SUM(total_sale) AS net_sale 
FROM retail_sales 
GROUP BY category;
```

### ✅ Average Customer Age in 'Beauty' Category

```sql
SELECT ROUND(AVG(age), 2) AS avg_age 
FROM retail_sales 
WHERE category = 'Beauty';
```

### ✅ High-Value Transactions

```sql
SELECT * FROM retail_sales WHERE total_sale > 1000;
```

### ✅ Gender-wise Transactions by Category

```sql
SELECT category, gender, COUNT(*) AS total_trans 
FROM retail_sales 
GROUP BY category, gender;
```

### ✅ Top Month of Each Year by Average Sales

```sql
SELECT year, month, avg_sale
FROM (
  SELECT 
    YEAR(sale_date) AS year,
    MONTH(sale_date) AS month,
    AVG(total_sale) AS avg_sale,
    RANK() OVER(PARTITION BY YEAR(sale_date) ORDER BY AVG(total_sale) DESC) AS rank
  FROM retail_sales
  GROUP BY year, month
) AS ranked_months
WHERE rank = 1;
```

### ✅ Top 5 Customers by Sales

```sql
SELECT customer_id, SUM(total_sale) AS total_sales 
FROM retail_sales 
GROUP BY customer_id 
ORDER BY total_sales DESC 
LIMIT 5;
```

---

## 📈 Key Insights

* Top product categories: Clothing and Beauty
* High-value purchases (over ₹1000) indicate strong buyer segments
* Sales vary across months – some clear high-performing periods
* Top 5 customers contribute significantly to revenue
* Shift-wise sales analysis shows peak times

---

## 🚀 How to Use

1. Clone this repository.
2. Import the `retail_sales.csv` into your MySQL database.
3. Execute queries from `sales_sqlquery.sql` in any SQL IDE or MySQL Workbench.

---

## 👨‍💻 Author

I’m learning SQL and data analysis on my own by following projects and tutorials. This project helped me understand key SQL techniques used by data analysts.

Feel free to explore or build upon this repo!


