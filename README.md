# 🍕 Pizza Sales SQL Analysis (KPIs)


## 📌 Project Overview
This project focuses on analyzing pizza sales data using **SQL Server** to extract critical Business Intelligence (BI) insights and Key Performance Indicators (KPIs). The analysis helps monitor sales performance, track order trends, and measure operational efficiency.

---

## 📊 Key Performance Indicators (KPIs) & Queries

### 1. Total Revenue
Calculates the total revenue generated from all pizza sales.
```sql
SELECT SUM(total_price) AS [Total Revenue] 
FROM pizza_sales;
```
<img width="188" height="76" alt="image" src="https://github.com/user-attachments/assets/5e180d45-734c-42ce-a784-ae45916ab1a7" />


### 2. Average Order Value
Finds the average amount spent per order.
```sql
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS [Average Order Value] 
FROM pizza_sales;
```
<img width="200" height="73" alt="image" src="https://github.com/user-attachments/assets/ca380ad2-212c-497e-9912-2ed94073be8c" />


### 3. Total Pizzas Sold
Sums up the total quantity of all pizzas sold.
```sql
SELECT SUM(quantity) AS [Total Pizza Sold] 
FROM pizza_sales;
```
<img width="181" height="82" alt="image" src="https://github.com/user-attachments/assets/0461c6dd-37f1-4dbc-9f63-eb4d638c0c86" />


### 4. Total Orders
Counts the total number of distinct orders placed.
```sql
SELECT COUNT(DISTINCT order_id) AS [Total Orders] 
FROM pizza_sales;
```
<img width="183" height="73" alt="image" src="https://github.com/user-attachments/assets/d2eb59e6-1e28-4531-b203-a83f3d6fc4d4" />


### 5. Average Pizzas Per Order
Calculates the average number of pizzas included in a single order.
```sql
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2)) AS [Average Pizza Per Orders] 
FROM pizza_sales;
```
<img width="229" height="81" alt="image" src="https://github.com/user-attachments/assets/c18c885d-2e53-4a04-882b-88ed8852f4a7" />

### 6. Daily Trend for Total Sales
Analyzes the total sales distribution across different days of the week to identify peak business days.
```sql
SELECT DATENAME(DW, order_date) AS 'DayName', 
       CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_sales
FROM pizza_sales
GROUP BY DATENAME(DW, order_date)
ORDER BY SUM(total_price) DESC;
```
<img width="245" height="230" alt="image" src="https://github.com/user-attachments/assets/ad9ad1ef-107f-406a-8073-a118a10e5318" />


### 7. Monthly Trend for Total Sales
Monitors sales performance on a monthly basis to identify seasonal trends and high-performing months.
```sql
SELECT DATENAME(MONTH, order_date) AS 'DayName', 
       CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_sales
FROM pizza_sales
GROUP BY DATENAME(MONTH, order_date)
ORDER BY SUM(total_price) DESC;
```
<img width="310" height="341" alt="image" src="https://github.com/user-attachments/assets/db447273-82a8-4b8f-89e6-2a6cc1e70a86" />


### 8. Percentage of Sales by Pizza Category
Calculates the total sales and the percentage contribution (PCT) of each pizza category to the overall revenue.
```sql
SELECT pizza_category, 
       CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_sales,
       CONVERT(DECIMAL(10,2), SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales)) AS PCT
FROM pizza_sales
GROUP BY pizza_category
ORDER BY SUM(total_price) DESC;
```
<img width="368" height="152" alt="image" src="https://github.com/user-attachments/assets/98c35875-061c-4496-987c-ff111f699dcd" />




---

## 🛠️ Technologies Used
* **Database:** Microsoft SQL Server
* **Language:** T-SQL

* **Database:** Microsoft SQL Server
* **Language:** T-SQL
