# 📊 Superstore Sales Revenue Analysis

## 📋 Project Overview
This project performs a deep dive into the Superstore Sales Dataset using SQL. Since the dataset focuses on sales transactions without profit margins, the analysis is centered on identifying high-growth regions, top-performing product categories, and customer segmentation to drive revenue growth.

## 🛠️ Tech Stack
* Language: SQL
* Platform: Google BigQuery
* Dataset: Superstore Sales (9,800+ rows)

---

## 🧹 1. Data Cleaning & Preparation
The first step was to ensure data integrity by checking for nulls and verifying the structure.

```sql

 Checking for null values in Sales and Order ID
SELECT 
    COUNT(*) AS total_rows,
    COUNT(Order_ID) AS non_null_orders,
    COUNT(Sales) AS non_null_sales
FROM `my_project.train`;
```

## 🔍 2. Business Insights (SQL Queries)

​Q1: Revenue Trends by Region
​Which geographical areas are generating the most revenue?

```sql
SELECT 
    Region, 
    ROUND(SUM(Sales), 2) AS Total_Sales,
    COUNT(DISTINCT Order_ID) AS Total_Orders,
    ROUND(SUM(Sales) / COUNT(DISTINCT Order_ID), 2) AS Avg_Order_Value
FROM my_project.train
GROUP BY Region
ORDER BY Total_Sales DESC;
```
Q2: Top Performing Categories & Sub-Categories
​Which products are the primary revenue drivers?

```sql
SELECT 
    Category, 
    Sub_Category, 
    ROUND(SUM(Sales), 2) AS Total_Sales
FROM my_project.train
GROUP BY Category, Sub_Category
ORDER BY Category, Total_Sales DESC;
```
Q3: Customer Segmentation Analysis
​Who are our top 10 customers by spending?

```sql
SELECT 
    Customer_Name, 
    Segment, 
    ROUND(SUM(Sales), 2) AS Total_Spent
FROM my_project.train
GROUP BY Customer_Name, Segment
ORDER BY Total_Spent DESC
LIMIT 10;
```
Q4: Yearly Sales Growth
​How is the business performing over time?

```sql
SELECT 
    EXTRACT(YEAR FROM Order_Date) AS Sales_Year,
    ROUND(SUM(Sales), 2) AS Annual_Revenue
FROM my_project.train
GROUP BY Sales_Year
ORDER BY Sales_Year;
```
---

## 💡 Strategic Recommendations

- **Focus on the West:**  
  The analysis shows high revenue density in the West region; expanding logistics there could further boost sales.

- **Category Growth:**  
  Technology and Furniture are top sellers. Marketing campaigns should lead with these categories.

- **High-Value Customers:**  
  A loyalty program targeting the **Corporate** segment could stabilize long-term revenue.
