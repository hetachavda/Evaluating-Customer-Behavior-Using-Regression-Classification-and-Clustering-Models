# 🚗 Classic Car Dealership Analytics  

A **data analytics project** leveraging SQL, visualization, and machine learning techniques to analyze **customer behavior, sales trends, and marketing performance** for a classic car dealership.  

This project was developed as part of **Data Analytics Case Study 1 (DAMO-501-3)**.  

---

## 📌 Project Overview  
The project applies data from the **Classic Models database** to answer key business questions such as:  
- Which **customer demographics** drive sales?  
- What are the **top-selling products** and seasonal trends?  
- How effective are **marketing campaigns** and employee contributions?  
- How can predictive models enhance **decision-making** and **marketing strategies**?  

---

## 🎯 Objectives  
- Analyze **customer demographics** and regional credit limits  
- Identify **top-selling products** and sales trends  
- Examine **seasonal and monthly demand patterns**  
- Evaluate **employee performance and workload distribution**  
- Build predictive models (**Regression, Classification, Clustering**) to support strategy  

---

## 📂 Dataset & SQL Queries  

The project uses the **Classic Models dataset** with key tables: `customers`, `orders`, `orderdetails`, `employees`, `offices`, `products`.  

### Example Queries  

```sql
-- Customer demographics by region
SELECT country, state, city, COUNT(customerNumber) AS num_customers,
       AVG(creditLimit) AS avg_credit_limit
FROM classicmodels.customers
GROUP BY country, state, city
ORDER BY num_customers DESC;

-- Top-selling products
SELECT p.productCode, p.productName,
       SUM(od.quantityOrdered * od.priceEach) AS total_sales
FROM classicmodels.orderdetails od
JOIN classicmodels.products p ON od.productCode = p.productCode
GROUP BY p.productCode, p.productName
ORDER BY total_sales DESC;

-- Monthly sales trends
SELECT YEAR(orderDate) AS year, MONTH(orderDate) AS month,
       SUM(od.quantityOrdered * od.priceEach) AS monthly_sales
FROM classicmodels.orders o
JOIN classicmodels.orderdetails od ON o.orderNumber = od.orderNumber
GROUP BY year, month
ORDER BY year, month;
