# ☕ CKARA Coffee: Data Engineering Project

A data engineering project simulating a real-world business scenario for a specialty coffee brand operating in Spain. This project focuses on designing and implementing a multi-layered **data warehouse** to unify data across sales, employee activity, and marketing engagement.

---

## 📌 Objectives

- Centralize disparate datasets into a unified, scalable **data warehouse**
- Build **ETL pipelines** using **Alteryx** to automate data transformation
- Support business KPIs across departments: Sales, Marketing, HR, and Operations
- Enable actionable analytics like product demand by region, employee performance, and social media ROI

---

## 🏗️ Tech Stack

- **ETL**: Alteryx
- **Data Modeling**: Star Schema
- **Database Design**: Fact and Dimension tables
- **Scripting**: SQL (for DDL & analysis)
- **BI Use Case**: Insights derived from DWH to support expansion and targeting strategy

---

## 🧱 Data Warehouse Structure

This project implements a **multi-domain DWH** composed of the following:

### 🟦 Fact Tables
- `SALES_FACT`: transactions, revenue, quantity, store
- `CLICKS_FACT`: clickstream events, browser, duration
- `EMPLOYEE_FACT`: employee performance, social media engagement

### 🟩 Dimension Tables
- `DATE_DIM`: day, month, year
- `EMPLOYEE_DIM`: name, role, location
- `PRODUCT_DIM`: SKU, origin, category
- `CUSTOMER_DIM`: segment, location
- `STORE_DIM`: city, region
- `CHANNEL_DIM`: marketing source (e.g., Instagram, Web)

---

## 🧪 Key Use Cases

- Identify high-performing products (e.g., 32% sales growth in Brazilian coffee)
- Detect underserved areas like **El Born** with high demand for "Instagrammable" coffee shops
- Correlate employee social media activity with store performance
- Optimize new store locations using combined sales + clickstream data

---

## 📊 Sample Query

```sql
-- Total sales by employee for Brazilian coffee in El Born
SELECT e.name, SUM(s.revenue) AS total_sales
FROM SALES_FACT s
JOIN EMPLOYEE_DIM e ON s.employee_id = e.employee_id
JOIN PRODUCT_DIM p ON s.product_id = p.product_id
JOIN STORE_DIM st ON s.store_id = st.store_id
WHERE p.origin = 'Brazil' AND st.neighborhood = 'El Born'
GROUP BY e.name
ORDER BY total_sales DESC;
