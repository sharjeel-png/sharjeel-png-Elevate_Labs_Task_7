# Task 7 – Basic Sales Summary using SQLite and Python

## Objective
The objective of this task is to use SQL inside Python to extract basic sales insights from a small SQLite database and visualize the results using a simple bar chart.

---

## Tools & Technologies
- Python  
- SQLite (sqlite3)  
- Pandas  
- Matplotlib  
- Google Colab  

---

## Project Files
- task7_sales_summary.ipynb – Main notebook  
- sales_data.db – SQLite database file  
- sales_chart.png – Revenue bar chart  
- README.md – Project documentation  

---

## Database Design
A single SQLite table named `sales` is used.

Table structure:

| Column Name    | Data Type | Description |
|---------------|----------|-------------|
| `sale_id`     | INTEGER  | Unique identifier for each sale (Primary Key) |
| `product`     | TEXT     | Name of the product |
| `quantity`    | INTEGER  | Number of units sold |
| `price`       | REAL     | Price per unit |
| `last_updated`| TEXT     | Timestamp of last insert or update |

The `sale_id` uniquely identifies each sale, and `last_updated` stores the timestamp of the last insert or update.

---

## Data Ingestion Logic (Incremental / UPSERT)
This project uses an incremental insert/update approach:

- If a sale_id does not exist, a new record is inserted  
- If a sale_id already exists, the record is updated  
- This prevents duplicate records and keeps data consistent  

SQLite’s `ON CONFLICT` (UPSERT) logic is used to implement this behavior.

**SQL UPSERT Example (SQLite)**

```sql
INSERT INTO sales (sale_id, product, quantity, price, last_updated)
VALUES (?, ?, ?, ?, CURRENT_TIMESTAMP)
ON CONFLICT(sale_id)
DO UPDATE SET
    product = excluded.product,
    quantity = excluded.quantity,
    price = excluded.price,
    last_updated = CURRENT_TIMESTAMP;
```
---

## SQL Sales Summary Query
The following SQL query is used to calculate total quantity sold and total revenue per product:

### Purpose
- Calculate total quantity sold per product  
- Calculate total revenue per product  

### Query

```sql
SELECT
    product,
    SUM(quantity) AS total_quantity,
    SUM(quantity * price) AS revenue
FROM sales
GROUP BY product;
```

## Data Visualization
- A bar chart is created to visualize revenue by product  
- The chart is displayed in the notebook  
- The chart is saved as `sales_chart.png` using matplotlib  

---

## How to Run the Project (Google Colab)
1. Open `task7_sales_summary.ipynb` in Google Colab  
2. Run all cells from top to bottom  
3. After execution, download:
   - sales_data.db  
   - sales_chart.png  
---

## Outcome
By completing this task, the following skills are demonstrated:
- Writing SQL queries with GROUP BY  
- Using SQLite inside Python  
- Handling incremental data updates  
- Loading SQL results into Pandas  
- Creating and saving basic visualizations  

---

## Notes
- The project is fully reproducible  
- Uploaded database and chart provide proof of SQL execution  
- The same code works in both Colab and local environments  

---

## Author
**Name:** MOHAMMAD SHARJEEL YAZDANI  
**Role:** Data Analyst Intern  
**Organization:** Elevate Labs  
**Date:** 19/12/2025

---

## Internship Company Name

This project was completed as part of a **Data Analyst Internship under Elevate Labs**

---

## Task Status
Completed successfully
