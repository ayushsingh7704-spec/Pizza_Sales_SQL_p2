# Pizza Sales Analysis SQL Project

## Project Overview

**Project Title**: Pizza Sales Analysis 

This project analyzes pizza sales data using SQL to extract meaningful business insights. It focuses on evaluating sales performance, revenue trends, customer preferences, and product popularity through structured data analysis.

By applying joins, aggregations, window functions, and time-based analysis, the project addresses real-world business questions and supports data-driven decision-making related to sales strategy and operational planning.

## Objectives

1. Analyze pizza sales data to understand order volume and revenue performance
2. Identify top-selling pizzas, popular sizes, and high-value products
3. Examine time-based and category-wise sales trends
4. Generate data-driven insights to support business decision-making
## Project Structure

### 1. Data Analysis & Findings

The following SQL queries were developed to answer specific business questions:

1. **Retrieve the total number of orders placed.**:
```sql
SELECT 
    COUNT(order_id) AS total_orders
FROM
    orders;
```

2. **Calculate the total revenue generated from pizza sales.**:
```sql
SELECT 
    round(sum(order_details.quantity * pizzas.price),2) as total_sales
FROM
    order_details
        JOIN
    pizzas ON pizzas.pizza_id = order_details.pizza_id
```

3. **Identify the highest-priced pizza.**:
```sql
SELECT 
    pizza_types.name, pizzas.price
FROM
    pizza_types
        JOIN
    pizzas ON pizza_types.pizza_type_id = pizzas.pizza_type_id
ORDER BY pizzas.price DESC
LIMIT 1;
```

4. **Identify the most common pizza size ordered.**:
```sql
SELECT 
    pizzas.size,
    COUNT(order_details.order_details_id) AS order_count
FROM
    pizzas
        JOIN
    order_details ON pizzas.pizza_id = order_details.pizza_id
GROUP BY pizzas.size
ORDER BY order_count DESC;
```

5. **List the top 5 most ordered pizza types along with their quantities..**:
```sql
SELECT 
    pizza_types.name, SUM(order_details.quantity) AS quantity
FROM
    pizza_types
        JOIN
    pizzas ON pizza_types.pizza_type_id + pizzas.pizza_type_id
        JOIN
    order_details ON order_details.pizza_id + pizzas.pizza_id
GROUP BY pizza_types.name
ORDER BY quantity DESC limit 5;
```

6. **Join the necessary tables to find the total quantity of each pizza category ordered.**:
```sql
SELECT 
    pizza_types.category,
    SUM(order_details.quantity) AS quantity
FROM
    pizza_types
        JOIN
    pizzas ON pizza_types.pizza_type_id = pizzas.pizza_type_id
        JOIN
    order_details ON order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_types.category
ORDER BY quantity DESC;
```

7. **Determine the distribution of orders by hour of the day.**:
```sql
SELECT 
    HOUR(order_time) AS hour, COUNT(order_id) AS order_count
FROM
    orders
GROUP BY HOUR(order_time);
```

8. **Join relevant tables to find the category-wise distribution of pizzas.**:
```sql
SELECT 
    AVG(quantity)
FROM
    (SELECT 
        orders.order_date, SUM(order_details.quantity) AS quantity
    FROM
        orders
    JOIN order_details ON orders.order_id = order_details.order_id
    GROUP BY orders.order_date) AS order_quantity;
```

9. **Determine the top 3 most ordered pizza types based on revenue.**:
```sql
SELECT 
    pizza_types.name,
    SUM(order_details.quantity * pizzas.price) AS revenue
FROM
    pizza_types
        JOIN
    pizzas ON pizzas.pizza_type_id = pizza_types.pizza_type_id
        JOIN
    order_details ON order_details.pizza_id = pizzas.pizza_id
GROUP BY pizza_types.name
ORDER BY revenue DESC
LIMIT 3;
```

10. **Analyze the cumulative revenue generated over time.**:
```sql
select order_date, 
sum(revenue) over(order by order_date) as cum_revenue
from
(select orders.order_date,
sum(order_details.quantity * pizzas.price) as revenue
from order_details join pizzas
on order_details.pizza_id = pizzas.pizza_id
join orders
on orders.order_id = order_details.order_id
group by orders.order_date) as sales;
```
10. **based on revenue for each pizza category.**:
```sql
select category, name, revenue, 
rank() over(partition by category order by revenue desc) as rn
from
(select pizza_types.category, pizza_types.name,
sum((order_details.quantity) * pizzas.price) as revenue
from pizza_types join pizzas
on pizza_types.pizza_type_id = pizzas.pizza_type_id
join order_details
on order_details.pizza_id = pizzas.pizza_id
group by pizza_types.category, pizza_types.name) as a;
```
## Key Findings

-A strong sales concentration was observed in a few top-performing pizza types, which contributed a significant share of total revenue.

-Large-sized pizzas were the most frequently ordered, indicating higher customer preference.

-Peak order volumes occurred during afternoon and evening hours, highlighting clear time-based demand patterns.

=Certain pizza categories consistently generated higher revenue, supporting focused product and inventory strategies.

Analytical Report 📝

The analysis was conducted using SQL by integrating multiple tables and applying aggregations, joins, window functions, and date-time operations. The study evaluated order volume, revenue trends, category-wise performance, and cumulative sales growth over time. Advanced queries enabled revenue contribution analysis and identification of top-performing pizzas across categories. The results provide a structured understanding of business performance and customer behavior.

Conclusion ✅

This project demonstrates the effective use of SQL as a business intelligence tool to analyze sales data and derive actionable insights. The findings can help businesses optimize pricing, inventory management, and sales strategies. Overall, the analysis supports data-driven decision-making and showcases practical SQL skills applicable to real-world business scenarios.

## Reports

-Generated sales and revenue reports to evaluate overall business performance

-Prepared category-wise and pizza-wise reports to identify top-performing products

=Created time-based reports (hourly and daily) to analyze ordering patterns

=Developed revenue contribution and cumulative revenue reports to support strategic decision-making
## Conclusion

This project demonstrates the effective use of SQL as a business intelligence tool to analyze sales data and derive actionable insights. The findings can help businesses optimize pricing, inventory management, and sales strategies. Overall, the analysis supports data-driven decision-making and showcases practical SQL skills applicable to real-world business scenarios.


- **LinkedIn**: [Connect with me professionally] (www.linkedin.com/in/iayushrajpoot)




