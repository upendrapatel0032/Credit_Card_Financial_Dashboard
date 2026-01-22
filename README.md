💳 Credit Card Financial Dashboard | Power BI & SQL

📌 Project Overview

The Credit Card Financial Dashboard is a Power BI project designed to provide weekly and year-to-date insights into credit card operations. The dashboard enables stakeholders to track revenue, transactions, customer behavior, and risk metrics using data stored in a SQL database.

This project demonstrates end-to-end data analytics skills, including data ingestion, SQL database management, DAX calculations, and interactive data visualization.
<img width="576" height="333" alt="{597E3112-4CE3-4310-9AF4-68A1BB013026}" src="https://github.com/user-attachments/assets/2d565026-9e52-420e-972a-f6906844d506" />
<img width="374" height="219" alt="{71D8E9D3-7D8B-4C65-B111-F1017D8070D7}" src="https://github.com/user-attachments/assets/5dc08b89-96e7-43ee-9743-3506056ecbc5" />

🎯 Project Objective

To develop a comprehensive weekly credit card dashboard that delivers:

Real-time monitoring of key performance metrics

Trend analysis across customers, revenue, and transactions

Actionable insights for data-driven decision-making


🛠️ Tech Stack

Database: PostgreSQL / SQL

Data Visualization: Power BI

Query Language: SQL

Analytics Language: DAX

Data Source: CSV files


📂 Dataset Description

The project uses two primary datasets:

Customer Details (cust_detail)

Credit Card Transaction Details (cc_detail)

These datasets include information such as customer demographics, income, card type, transaction amount, interest earned, and weekly activity.


🔄 Data Pipeline
1. Prepare CSV Files

Cleaned and structured raw customer and transaction data

Ensured correct date formats and column naming

2. Create SQL Tables

Designed relational tables for customer and credit card details

Applied appropriate data types and constraints

3. Import Data into SQL

Used COPY command to load CSV data into PostgreSQL

Validated data integrity after import


📐 DAX Calculations
🔹 Customer Segmentation

Age Group
AgeGroup = SWITCH(
 TRUE(),
 'public cust_detail'[customer_age] < 30, "20-30",
 'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
 'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
 'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
 'public cust_detail'[customer_age] >= 60, "60+",
 "Unknown"
)


Income Group
IncomeGroup = SWITCH(
 TRUE(),
 'public cust_detail'[income] < 35000, "Low",
 'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] < 70000, "Medium",
 'public cust_detail'[income] >= 70000, "High",
 "Unknown"
)

🔹 Revenue & Weekly Metrics
Week_Num = WEEKNUM('public cc_detail'[week_start_date])

Revenue = 
'public cc_detail'[annual_fees] + 
'public cc_detail'[total_trans_amt] + 
'public cc_detail'[interest_earned]

Current_Week_Revenue = 
CALCULATE(
 SUM('public cc_detail'[Revenue]),
 FILTER(
  ALL('public cc_detail'),
  'public cc_detail'[Week_Num] = MAX('public cc_detail'[Week_Num])
 )
)

Previous_Week_Revenue = 
CALCULATE(
 SUM('public cc_detail'[Revenue]),
 FILTER(
  ALL('public cc_detail'),
  'public cc_detail'[Week_Num] = MAX('public cc_detail'[Week_Num]) - 1
 )
)


📊 Key Insights (Week 53 – 31st Dec)
📈 Week-over-Week Change

Revenue increased by 28.8%

Total transaction amount & count showed significant growth

Customer count increased compared to the previous week

📅 Year-to-Date Overview

Total Revenue: 57M

Total Interest Earned: 8M

Total Transaction Amount: 46M

Male Customers: 31M revenue

Female Customers: 26M revenue

Blue & Silver Cards: 93% of total transactions

Top States (TX, NY, CA): 68% of total contribution


⚠️ Risk & Activation Metrics

Overall Activation Rate: 57.5%

Overall Delinquent Rate: 6.06%

📌 Dashboard Features

Weekly & YTD performance tracking

Customer segmentation by age, income, gender, and region

Revenue and transaction trend analysis

Card-type and state-wise contribution analysis

Risk metrics (activation & delinquency rates)

🚀 Future Enhancements

Automate data refresh using scheduled pipelines

Add predictive analysis for delinquency risk

Include monthly and quarterly trend comparisons

