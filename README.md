# Credit Card Financial Dashboard

This project involves the development of a comprehensive **Credit Card Financial Dashboard** using **Power BI**, with data sourced from a **SQL database**. The dashboard is designed to provide **real-time insights** into key performance metrics and trends to support data-driven decision-making for credit card operations.

---

## 📊 Project Objective

To create a user-friendly and dynamic dashboard that helps stakeholders monitor credit card operations through interactive visualizations and real-time analytics.

---

## 🛠️ Tools & Technologies

- **Power BI** – for dashboard design and data visualization
- **SQL Server** – for data extraction and querying
- **DAX (Data Analysis Expressions)** – for creating calculated columns and measures
- **Power Query** – for data cleaning and transformation

---

## 📈 Key Features

- **Interactive Dashboard:** Drill-down capabilities to analyze data weekly, by customer segment, region, or transaction type.
- **Real-time KPIs:** Visual tracking of key metrics like:
  - Total transaction volume
  - Average spend per customer
  - Approval and rejection rates
  - Customer activity trends
- **Filters & Slicers:** Flexible filtering by time period, customer type, and card type for custom analysis.
- **Automated Refresh:** Integrated data pipelines for seamless updates with minimal manual effort.

---

## 📁 Data Overview

> **Note:** Sample or anonymized data used to preserve privacy. If you're viewing this as a template, replace with your own dataset.

- **Transaction Table:** Transaction ID, Date, Amount, Card Type, Status
- **Customer Table:** Customer ID, Region, Age Group, Credit Score, Account Status

---

## 📌 Use Cases

- Monitor and optimize **credit card usage and customer engagement**
- Track **approval trends and spending behavior**
- Identify **regions or periods** with unusual activity or performance drops
- Provide stakeholders with **self-service BI insights**

---
Below are the SQL scripts used to set up the database, create tables, and import CSV data into PostgreSQL:

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

-- 3. Import data from CSV files (update path based on your system)
-- cc_detail table
COPY cc_detail
FROM 'D:\credit_card.csv' 
DELIMITER ',' 
CSV HEADER;

-- cust_detail table
COPY cust_detail
FROM 'D:\customer.csv' 
DELIMITER ',' 
CSV HEADER;

-- ✅ Tip: If you encounter the error below:
-- ERROR:  date/time field value out of range: "0"
-- HINT: Perhaps you need a different "datestyle" setting.

-- Try this before the COPY command:
SET datestyle TO 'ISO, DMY';

-- 4. Insert additional weekly data
COPY cc_detail
FROM 'D:\cc_add.csv' 
DELIMITER ',' 
CSV HEADER;

COPY cust_detail
FROM 'D:\cust_add.csv' 
DELIMITER ',' 
CSV HEADER;


## 🧠 Learnings & Impact

- Applied advanced **DAX** formulas to derive performance KPIs
- Built automated, refreshable workflows using **Power Query**
- Improved stakeholder decision-making through **visual storytelling and data transparency**

---

## 📷 Screenshots

> *(Include visuals of your dashboard here — upload PNG or JPEG files and use the following markdown to embed them)*

```markdown
![Dashboard Overview](images/dashboard-overview.png)
![Customer Insights](images/customer-insights.png)
