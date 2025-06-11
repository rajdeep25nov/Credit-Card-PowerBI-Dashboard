# 💳 Credit Card Financial Dashboard – Power BI

This project showcases a **Credit Card Financial Dashboard** built using **Power BI**, powered by customer and transaction data from a **PostgreSQL database**. The dashboard provides **real-time insights** into key financial and operational metrics, enabling stakeholders to make informed decisions.

---

## 🎯 Objective

To develop a comprehensive dashboard that helps monitor and analyze weekly trends in credit card usage, customer behavior, and financial performance.

---

## 🛠️ Tools & Technologies

- **Power BI** – for interactive visualizations and reporting
- **PostgreSQL (SQL)** – for data storage, querying, and management
- **DAX (Data Analysis Expressions)** – for calculated columns, KPIs, and custom measures
- **Power Query** – for data cleaning and transformation

---

## 📈 Key Features

- 📊 **Interactive Dashboard** – Drill-down features and dynamic slicers for detailed analysis
- 🧮 **KPI Tracking** – Metrics like:
  - Total Transaction Volume
  - Average Spend per Customer
  - Approval & Rejection Rates
  - Credit Utilization Ratio
- 🔄 **Automated Data Refresh** – Using Power Query to enable efficient data loading
- 📍 **Custom Filters** – Time-based, demographic-based, and card-type-based filters for user-specific insights

---

## 📁 Data Overview

The project utilizes two datasets:

- **creditcard.csv** – Weekly credit card transaction details
- **customer.csv** – Customer demographic and financial data

Key fields include:
- `Total_Trans_Amt`, `Total_Trans_Ct`, `Credit_Limit`, `Card_Category`, `Customer_Age`, `Income`, `Customer_Job`, etc.

---

## 🧠 Insights & Impact

- Enabled stakeholders to track and respond to usage patterns, customer behavior, and high-risk accounts.
- Identified spending trends and approval rates, supporting credit policy adjustments.
- Improved reporting efficiency with automated refresh and clean visual storytelling.

---

## 📌 Use Cases

- Business performance tracking across time and customer segments
- Identifying growth opportunities or risk zones in card usage
- Financial planning and resource allocation

---

## 💻 SQL Setup & Data Import

<details>
<summary><strong>SQL Queries to Create Tables and Import Data</strong></summary>

```sql
-- 0. Create a new database
CREATE DATABASE ccdb;

-- 1. Create the cc_detail table
CREATE TABLE cc_detail (
    Client_Num INT,
    Card_Category VARCHAR(20),
    Annual_Fees INT,
    Activation_30_Days INT,
    Customer_Acq_Cost INT,
    Week_Start_Date DATE,
    Week_Num VARCHAR(20),
    Qtr VARCHAR(10),
    current_year INT,
    Credit_Limit DECIMAL(10,2),
    Total_Revolving_Bal INT,
    Total_Trans_Amt INT,
    Total_Trans_Ct INT,
    Avg_Utilization_Ratio DECIMAL(10,3),
    Use_Chip VARCHAR(10),
    Exp_Type VARCHAR(50),
    Interest_Earned DECIMAL(10,3),
    Delinquent_Acc VARCHAR(5)
);

-- 2. Create the cust_detail table
CREATE TABLE cust_detail (
    Client_Num INT,
    Customer_Age INT,
    Gender VARCHAR(5),
    Dependent_Count INT,
    Education_Level VARCHAR(50),
    Marital_Status VARCHAR(20),
    State_cd VARCHAR(50),
    Zipcode VARCHAR(20),
    Car_Owner VARCHAR(5),
    House_Owner VARCHAR(5),
    Personal_Loan VARCHAR(5),
    Contact VARCHAR(50),
    Customer_Job VARCHAR(50),
    Income INT,
    Cust_Satisfaction_Score INT
);

-- 3. Import data from CSV (update file paths)
COPY cc_detail
FROM 'D:\credit_card.csv' 
DELIMITER ',' 
CSV HEADER;

COPY cust_detail
FROM 'D:\customer.csv' 
DELIMITER ',' 
CSV HEADER;

-- Optional: Handle date format errors
SET datestyle TO 'ISO, DMY';

-- 4. Import additional weekly data
COPY cc_detail
FROM 'D:\cc_add.csv' 
DELIMITER ',' 
CSV HEADER;

COPY cust_detail
FROM 'D:\cust_add.csv' 
DELIMITER ',' 
CSV HEADER;
