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
    COUNT(`Order ID`) AS non_null_orders,
    COUNT(Sales) AS non_null_sales
FROM hardy-messenger-472122-c1.my_project.superstore_sales`Order ID`
```
<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/fba7791f-cf12-4325-9c90-cd92e2be6994" />

### SQL Implementation (BigQuery)
To ensure data quality, I performed an audit for duplicates and verified the key metrics against the raw dataset:

```sql
-- Checking for duplicate orders
SELECT `Order ID`, `Product ID`, COUNT(*)
FROM `hardy-messenger-472122-c1.my_project.superstore_sales`
GROUP BY `Order ID`, `Product ID`
HAVING COUNT(*) > 1;
```
<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/b63b69b3-5d20-4906-81b7-b157c8efd9d9" />

```sql
-- Verifying annual sales performance
SELECT EXTRACT(YEAR FROM Order_Date) AS Year, SUM(Sales) AS Annual_Sales
FROM `hardy-messenger-472122-c1.my_project.superstore_sales`
GROUP BY Year
ORDER BY Year;
```
<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/4c7ec686-b42c-4795-8199-4f8188ac7dc9" />

### 🔎 Data Quality Check Results:
After running the initial cleaning query, the results confirmed that the dataset is highly reliable:
* Total Rows: 9,800
* Non-Null Order IDs: 9,800
* Non-Null Sales: 9,800

Conclusion: There are no missing values in the critical columns, allowing for an accurate revenue analysis without the need to drop or impute data.

## 🔍 2. Business Insights (SQL Queries)

​Q1: Revenue Trends by Region
​Which geographical areas are generating the most revenue?

```sql
SELECT 
    Region, 
    ROUND(SUM(Sales), 2) AS Total_Sales,
    COUNT(DISTINCT `Order ID`) AS Total_Orders,
    ROUND(SUM(Sales) / COUNT(DISTINCT `Order ID`), 2) AS Avg_Order_Value
FROM hardy-messenger-472122-c1.my_project.superstore_sales
GROUP BY Region
ORDER BY Total_Sales DESC;
```
<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/34bad90b-aceb-4ccb-b20a-defb51ba901b" />

#### 📊 Key Findings & Insights
- Top Region: West with $710,219.68 in total revenue.
- Highest Efficiency: East Region leads with an Avg Order Value of $489.06.
- Order Volume: West processed 1,587 orders, the highest across all regions.
- Growth Area: South Region is the lowest performer ($389,151.46 revenue).

Q2: Top Performing Categories & Sub-Categories
​Which products are the primary revenue drivers?

```sql
SELECT 
    Category, 
    `Sub-Category`, 
    ROUND(SUM(Sales), 2) AS Total_Sales
FROM hardy-messenger-472122-c1.my_project.superstore_sales
GROUP BY Category, `Sub-Category`
ORDER BY Category, Total_Sales DESC;
```
<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/58a64924-97a7-47b3-83ce-4c0f712ec50d" />

#### 📦 Key Category Insights
- Top Sub-Category: Phones (Technology) is a major driver with $327,782.45 in sales.
- Strong Performance: Chairs (Furniture) follows closely with $322,822.73 in revenue.
- Bulk Sales: Binders and Storage are the top sub-categories in Office Supplies.
- Low-Value Items: Fasteners and Envelopes contribute the least to the overall revenue.

Q3: Customer Segmentation Analysis
​Who are our top 10 customers by spending?

```sql
SELECT 
   `Customer Name` 
    Segment, 
    ROUND(SUM(Sales), 2) AS Total_Spent
FROM hardy-messenger-472122-c1.my_project.superstore_sales
GROUP BY `Customer Name`, Segment
ORDER BY Total_Spent DESC
LIMIT 10;
```
<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/ada8d843-9127-4beb-918e-eaace9913285" />
<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/2be83303-129e-4f74-a4a9-d47d70bbf845" />

#### 👤 Key Customer Insights
- Top Spender: Sean Miller is the highest-value customer with $25,043.05 spent.
- Elite Tier: The top 3 customers (Sean, Tamara, and Raymond) have each spent over $15,000.
- Customer Base: The top 10 customers collectively contribute a significant portion of individual high-ticket sales.

Q4: Yearly Sales Growth
​How is the business performing over time?

```sql
SELECT 
    EXTRACT(YEAR FROM `Order Date`) AS Sales_Year,
    ROUND(SUM(Sales), 2) AS Annual_Revenue
FROM hardy-messenger-472122-c1.my_project.superstore_sales
GROUP BY Sales_Year
ORDER BY Sales_Year;
```
<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/7f8c9e3a-2bab-4ef7-9cae-21b126125f4f" />

#### 📈 Yearly Performance Insights
- Peak Year: 2018 was the highest revenue year with $722,052.02.
- Growth Trend: Sales jumped significantly from $459,436.01 in 2016 to $600,192.55 in 2017.
- Initial Performance: The business started strong in 2015 with $479,856.21 in total revenue.
- Consistent Upward Momentum: The data shows a clear year-over-year increase starting from 2016.
---

## 💡 Strategic Recommendations

Based on the final data analysis of 9,800 records, the following strategic actions are recommended:

* Regional Market Optimization:
    * Maximize West Region Dominance: As the primary revenue driver with $710,219.68, we should expand logistics and warehouse capacity in the West to maintain this lead.
    * Target High-Spenders in the East: Since the East region has the highest Average Order Value ($489.06), marketing should focus on "Premium Product" bundles for this segment.

* Product Strategy:
    * Inventory Priority: Prioritize stock for Phones ($327,782.45) and Chairs ($322,822.73), as they are the top-performing sub-categories.
    * Review Low-Contribution Items: Re-evaluate the viability of Fasteners ($3,001.96), as their revenue contribution is minimal.

* Customer Retention:
    * High-Value Loyalty Program: Launch a VIP program for elite customers like Sean Miller ($25,043.05) and Tamara Chand ($19,052.22) to ensure long-term retention.

* Growth Momentum:
    * Replicate 2018 Success: With revenue peaking at $722,052.02 in 2018, the business should analyze and replicate the promotional strategies used during that year for future planning.
      
      ---
      
      🔗 View the Interactive Dashboard on Tableau Public: [https://public.tableau.com/views/USSuperstoreSalesAnalysis-PortfolioProject/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link].
