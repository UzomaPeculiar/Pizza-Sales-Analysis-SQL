# Pizza Sales Analysis SQL Project

## Project Overview

**Project Title**: Pizza Sales Analysis  
**Database**: `pizza_db`

This project demonstrates SQL skills and techniques used by data analysts to explore, clean, and analyze pizza sales data. The project involves setting up a pizza sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries.


## Project Structure

### 1. Database Setup

- **Database Creation**: The project starts by creating a database named `pizza_db`.


### 2. Data Exploration & Cleaning

- **View All Records**
```sql
SELECT * FROM pizza_sales;
```

- **Total Revenue**
```sql
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
```

- **Average Order Value**
```sql
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales;
```

- **Total Pizzas Sold**
```sql
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;
```

- **Total Orders**
```sql
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales;
```

- **Average Pizzas Per Order**
```sql
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10, 2)) / CAST(COUNT(DISTINCT order_id) AS DECIMAL(10, 2)) AS DECIMAL(10, 2)) AS Avg_Pizzas_per_order
FROM pizza_sales;
```

### 3. Data Analysis & Findings

The following SQL queries were developed to answer specific business questions:

1. **Daily Trend for Total Orders**
```sql
SELECT 
    DATE_FORMAT(STR_TO_DATE(order_date, '%d-%m-%Y'), '%W') AS order_day,
    COUNT(DISTINCT order_id) AS total_orders
FROM pizza_sales
GROUP BY order_day;
```

2. **Monthly Trend for Orders**
```sql
SELECT 
    DATE_FORMAT(STR_TO_DATE(order_date, '%d-%m-%Y'), '%M') AS Month_Name,
    COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY Month_Name
ORDER BY Total_Orders DESC;
```

3. **Percentage of Sales by Pizza Category**
```sql
SELECT 
    pizza_category,
    CAST(SUM(total_price) AS DECIMAL(10, 2)) AS total_revenue,
    CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10, 2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category;
```

4. **Percentage of Sales by Pizza Size**
```sql
SELECT 
    pizza_size,
    CAST(SUM(total_price) AS DECIMAL(10, 2)) AS total_revenue,
    CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10, 2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;
```

5. **Total Pizzas Sold by Category**
```sql
SELECT pizza_category, SUM(quantity) AS Total_Quantity_Sold
FROM pizza_sales
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;
```

6. **Top 5 Pizzas by Revenue**
```sql
SELECT pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC
LIMIT 5;
```

7. **Bottom 5 Pizzas by Revenue**
```sql
SELECT pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC
LIMIT 5;
```

8. **Top 5 Pizzas by Quantity**
```sql
SELECT pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC
LIMIT 5;
```

9. **Bottom 5 Pizzas by Quantity**
```sql
SELECT pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
LIMIT 5;
```

10. **Top 5 Pizzas by Total Orders**
```sql
SELECT pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC
LIMIT 5;
```

11. **Bottom 5 Pizzas by Total Orders**
```sql
SELECT pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC
LIMIT 5;
```

12. **Top 5 Classic Pizzas by Total Orders**
```sql
SELECT pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
WHERE pizza_category = 'Classic'
GROUP BY pizza_name
ORDER BY Total_Orders DESC
LIMIT 5;
```

13. **Bottom 5 Classic Pizzas by Total Orders**
```sql
SELECT pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
WHERE pizza_category = 'Classic'
GROUP BY pizza_name
ORDER BY Total_Orders ASC
LIMIT 5;
```

## Findings

- **Revenue Insights**: The analysis shows total revenue, top-performing pizzas, and underperforming items.
- **Customer Preferences**: Larger-sized pizzas contribute significantly to revenue.
- **Sales Trends**: Certain months and days generate higher order volumes, showing clear seasonal patterns.
- **Category Performance**: Classic pizzas dominate total orders, while some premium pizzas contribute the highest revenue.

## Reports

- **Sales Summary**: A detailed overview of revenue, orders, and pizza quantities.
- **Trend Analysis**: Insights into monthly and daily order patterns.
- **Top & Bottom Performers**: Lists of best and worst-selling pizzas by revenue, quantity, and total orders.
