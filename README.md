# Credit Card Financial Risk Analysis Dashboard Project

## Overview
This Power BI dashboard provides real-time insights into credit card transactions and customer data. It helps monitor key performance metrics and trends, supporting decision-making processes.

## Features
- **Interactive Dashboard:** Developed using Power BI to visualize transaction and customer data.
- **Data Processing & Analysis:** Streamlined processes to ensure accurate and efficient data handling.
- **Actionable Insights:** Provided stakeholders with insights to support decision-making processes.

## Data Sources
- SQL database containing transaction and customer data.

## Key Metrics
- Total Transactions
- Customer Demographics
- Spending Trends
- Credit Card Utilization

## DAX Queries
```sql
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
    'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] < 70000, "Med",
    'public cust_detail'[income] >= 70000, "High",
    "unknown"
)
week_num2 = WEEKNUM('public cc_detail'[week_start_date])
Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]
Current_week_Reveneue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
    )
)
Previous_week_Reveneue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1
    )
)
```
## Project Insights
- **Week On Week change:**
  - Revenue increased by 28.8%
  - Total Transaction Amount & Count increased by xx% & xx%
  - Customer count increased by xx%
- **Overview Year To Date:**
  - Overall revenue is 57M
  - Total interest is 8M
  - Total transaction amount is 46M
  - Male customers contributing more in revenue: 31M, female: 26M
  - Blue & Silver credit card contributing to 93% of overall transactions
  - TX, NY & CA contributing to 68%
  - Overall Activation rate is 57.5%
  - Overall Delinquent rate is 6.06%
