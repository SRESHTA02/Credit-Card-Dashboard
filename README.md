# Credit-Card-Dashboard
PowerBI

## Content in this Project
1. Project Objective
2. Data from SQL
3. Data Processing & DAX
4. Dashboard & Insights
5. Export & Share Project

## Project Objective
To develop a comprehensive credit card weekly dashboard that provides real-time insights into key performance metrics and trends, enabling stakeholders to monitor and analyze credit card operations effectively.

## Data from SQL
Import data to SQL database.

## Data Processing & DAX
### DAX Queries
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

IncomeGroup = SWITCH(
 TRUE(),
 'public cust_detail'[income] < 35000, "Low",
 'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] <70000, "Med",
 'public cust_detail'[income] >= 70000, "High",
 "unknown"
)

week_num2 = WEEKNUM('public cc_detail'[week_start_date])

Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]

Current_week_Revenue = CALCULATE(
 SUM('public cc_detail'[Revenue]),
 FILTER(
 ALL('public cc_detail'),
 'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
))

Previous_week_Revenue = CALCULATE(
 SUM('public cc_detail'[Revenue]),
 FILTER(
 ALL('public cc_detail'),
 'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2]) - 1
))
```
## Dashboard & Insights
### Project Insights - Week 53 (31st Dec)

#### WoW Change:
- Revenue increased by 28.8%
- Total Transaction Amount & Count increased by xx% & xx%
- Customer count increased by xx%

#### Overview YTD:
- Overall revenue is 57M
- Total interest is 8M
- Total transaction amount is 46M
- Male customers are contributing more in revenue: 31M, female: 26M
- Blue & Silver credit cards are contributing to 93% of overall transactions
- TX, NY & CA are contributing to 68%
- Overall Activation rate is 57.5%
- Overall Delinquent rate is 6.06%

