# Credit-Card-Financial-Dashboard

![5fb298a9-8623-4bc0-8bc5-92fc1115de16](https://github.com/user-attachments/assets/4eb9bf1d-7dd8-46ed-a733-50c65f000499)

## Overview

This project aims to develop a **comprehensive credit card weekly dashboard** using Power BI. The dashboard provides real-time insights into key performance metrics and trends related to credit card operations, enabling stakeholders to make informed decisions. The data for this dashboard is sourced from a SQL database, and the project includes data import, transformation, and visualization using DAX queries and Power BI’s interactive dashboard features.

## Project Objective

The primary objective of this project is to:

- **Monitor credit card operations** by providing real-time insights into key performance metrics.
- Enable stakeholders to **analyze trends** and monitor financial performance.
- Facilitate **actionable insights** to support strategic decision-making processes.

## Data Import and Preparation

1. **CSV File Preparation**:
   - Data related to customers and credit card operations, such as customer demographics, annual fees, transactions, and interest earned, is stored in CSV files.

2. **SQL Database**:
   - Tables for customer details and credit card transactions were created in SQL.
   - The CSV files were then imported into these SQL tables, ensuring a structured and normalized dataset.

## DAX Queries Used in Power BI

Several DAX queries were employed to create calculated columns and metrics for analysis:

1. **Age Group Calculation**:
   ```DAX
   AgeGroup = SWITCH(
     TRUE(),
     'public cust_detail'[customer_age] < 30, "20-30",
     'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
     'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
     'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
     'public cust_detail'[customer_age] >= 60, "60+",
     "unknown"
   )
   ```

2. **Income Group Calculation**:
   ```DAX
   IncomeGroup = SWITCH(
     TRUE(),
     'public cust_detail'[income] < 35000, "Low",
     'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] < 70000, "Med",
     'public cust_detail'[income] >= 70000, "High",
     "unknown"
   )
   ```

3. **Revenue Calculation**:
   ```DAX
   Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]
   ```

4. **Current and Previous Week's Revenue**:
   ```DAX
   Current_week_Revenue = CALCULATE(
     SUM('public cc_detail'[Revenue]),
     FILTER(
       ALL('public cc_detail'),
       'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2]))
   )

   Previous_week_Revenue = CALCULATE(
     SUM('public cc_detail'[Revenue]),
     FILTER(
       ALL('public cc_detail'),
       'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1))
   ```
   
## Project Insights (Week 53 - 31st December)

- **Week-over-Week (WoW) change**:
  - Revenue increased by 28.8%.
  - Total transaction amount and count increased by **xx%** and **xx%** (to be calculated from real data).
  - Customer count increased by **xx%**.

- **Year-to-Date (YTD) Overview**:
  - Overall revenue: **$57M**.
  - Total interest earned: **$8M**.
  - Total transaction amount: **$46M**.
  - Revenue contribution: **Male customers $31M**, Female customers $26M.
  - **Blue & Silver** credit cards accounted for **93%** of overall transactions.
  - **TX, NY, and CA** contributed **68%** of total transactions.
  - **Overall Activation rate**: 57.5%.
  - **Overall Delinquent rate**: 6.06%.

## Power BI Dashboard

The Power BI dashboard integrates **real-time transaction and customer data** from the SQL database. The dashboard highlights:

- **Revenue trends** and **customer behavior** based on demographics (age, income).
- **Transaction details** broken down by card type, location, and customer segmentation.
- Key financial metrics such as total transaction amounts, customer counts, and delinquency rates.
- Visualizations to facilitate comparison of current and previous week's performance.

**Credit Card Transaction Report**
![image](https://github.com/user-attachments/assets/b8f33ca9-8d6a-43fb-a61a-d42ce221ca12)

**Credit Card Customer Report**
![image](https://github.com/user-attachments/assets/7454132b-8c6f-4709-8364-df1495c4b55c)



The **interactive visualizations** and **filters** in Power BI allow stakeholders to drill down into specific metrics and regions, providing insights into areas requiring attention.
