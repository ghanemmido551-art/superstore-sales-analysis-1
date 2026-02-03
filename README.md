# Superstore Sales Analysis

## Business Problem
Analyze retail sales data to identify profitable and loss-making regions, categories, and products, and provide actionable recommendations to improve overall profitability.

---

## Questions to Answer
1. Which regions are most and least profitable?  
2. Which product categories or sub-categories are profitable or unprofitable?  
3. What is the impact of discounts on profit?  
4. What are the top-performing products in terms of profit?

---

## Dataset
- Columns: OrderID, CustomerName, Region, Category, SubCategory, ProductName, Sales, Quantity, Discount, Profit  
- Rows: ~50,000 (Superstore Sales Dataset)  

---

## Analysis Steps
### 1. Data Cleaning
- Remove duplicates and NULL values.  
- Ensure column types are correct (numeric for Sales, Profit, Discount).  

### 2. SQL Queries
Total Sales & Profit
`sql
SELECT Region,
       SUM(Sales) AS total_sales,
       SUM(Profit) AS total_profit
FROM orders
GROUP BY Region
ORDER BY total_profit DESC;
SELECT Category,
       SUM(Sales) AS total_sales,
       SUM(Profit) AS total_profit
FROM orders
GROUP BY Category
ORDER BY total_profit DESC;
SELECT ProductName,
       SUM(Profit) AS total_profit
FROM orders
GROUP BY ProductName
ORDER BY total_profit DESC
LIMIT 10;
SELECT Discount,
       AVG(Profit) AS avg_profit
FROM orders
GROUP BY Discount
ORDER BY Discount;
SELECT SUM(Sales) AS total_sales,
       SUM(Profit) AS total_profit
FROM orders;
