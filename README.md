# 🛒 Superstore Sales Analysis (SQL Project)

## 📋 Project Overview
This project involves a comprehensive analysis of the Superstore Sales Dataset. The primary goal is to identify sales trends, evaluate profitability across different regions and categories, and provide data-driven recommendations to improve business performance.

## 🛠️ Tools Used
* Data Source: Superstore Sales Dataset (~10k rows)
* Environment: Google BigQuery (SQL)
* Key Skills: Data Cleaning, Aggregations, Grouping, and Performance Insights.

---

## 🧹 1. Data Cleaning
Before analysis, I ensured the data quality by checking for null values in critical columns like Sales and Profit.

`sql
-- Checking for missing values in core metrics
SELECT 
    COUNT(*) - COUNT(Order_ID) AS missing_order_id,
    COUNT(*) - COUNT(Sales) AS missing_sales,
    COUNT(*) - COUNT(Profit) AS missing_profit
FROM `my_project.train`;
Mohamed mostafa, [2/3/2026 8:59 PM]
SELECT 
    Region, 
    ROUND(SUM(Sales), 2) AS Total_Sales, 
    ROUND(SUM(Profit), 2) AS Total_Profit
FROM my_project.train
GROUP BY Region
ORDER BY Total_Profit DESC;

Mohamed mostafa, [2/3/2026 8:59 PM]
SELECT 
    Category, 
    ROUND(SUM(Sales), 2) AS Total_Sales, 
    ROUND(SUM(Profit), 2) AS Total_Profit,
    ROUND((SUM(Profit) / SUM(Sales)) * 100, 2) AS Profit_Margin_Percentage
FROM my_project.train
GROUP BY Category
ORDER BY Total_Profit DESC;

Mohamed mostafa, [2/3/2026 8:59 PM]
SELECT 
    Discount, 
    AVG(Profit) AS Avg_Profit, 
    COUNT(*) AS Number_of_Orders
FROM my_project.train
GROUP BY Discount
ORDER BY Discount ASC;

Mohamed mostafa, [2/3/2026 8:59 PM]
SELECT 
    Product_Name, 
    SUM(Sales) AS Total_Sales, 
    SUM(Profit) AS Total_Profit
FROM my_project.train
GROUP BY Product_Name
ORDER BY Total_Profit DESC
LIMIT 10;
