# 💳 Credit Card Financial Risk Analysis

<div align="center">

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=postgresql&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-E03A3E?style=for-the-badge&logo=microsoft&logoColor=white)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)

**An end-to-end financial risk analytics solution built with Power BI, SQL, and DAX — delivering real-time insights into credit card transactions, customer behavior, and revenue performance.**

</div>

---

## 🌐 Live Dashboard

> 🔴 **Click the banner below to access the interactive Power BI dashboard live:**

<div align="center">

[![Live Dashboard](https://img.shields.io/badge/🚀%20View%20Live%20Dashboard-Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://app.powerbi.com/reportEmbed?reportId=36663983-c32d-4ce4-b5ae-86ffebe668f3&autoAuth=true&ctid=2e589d81-ea7a-4dc7-8fb2-84ba95cc947f)

**[👉 Open Interactive Dashboard](https://app.powerbi.com/reportEmbed?reportId=36663983-c32d-4ce4-b5ae-86ffebe668f3&autoAuth=true&ctid=2e589d81-ea7a-4dc7-8fb2-84ba95cc947f)**

</div>

> ⚠️ _Access may require organizational credentials. The dashboard is hosted on Microsoft Power BI Service._

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Live Dashboard](#-live-dashboard)
- [Key Metrics & Insights](#-key-metrics--insights)
- [Features](#-features)
- [Data Sources](#-data-sources)
- [DAX Queries](#-dax-queries)
- [Project Insights](#-project-insights)
- [Tech Stack](#-tech-stack)
- [Author](#-author)

---

## 📌 Overview

This project presents a comprehensive **Credit Card Financial Risk Analysis Dashboard** built using **Power BI**, connected to a **SQL database** containing real-world-style transaction and customer data.

The dashboard empowers financial analysts, risk managers, and business stakeholders to:

- 📊 **Monitor** credit card revenue, transactions, and utilization in real time
- 🔍 **Identify** high-risk customer segments and delinquency patterns
- 📈 **Track** weekly and year-to-date performance trends
- 🌍 **Analyze** geographic and demographic revenue distribution

---

## 📊 Key Metrics & Insights

### 📅 Year-To-Date (YTD) Summary

| Metric | Value |
|---|---|
| 💰 Overall Revenue | **$57M** |
| 💵 Total Interest Earned | **$8M** |
| 🔄 Total Transaction Amount | **$46M** |
| 👨 Male Customer Revenue | **$31M** |
| 👩 Female Customer Revenue | **$26M** |
| 💳 Blue & Silver Card Share | **93%** of transactions |
| 🗺️ Top States (TX, NY, CA) | **68%** of revenue |
| ✅ Overall Activation Rate | **57.5%** |
| ⚠️ Overall Delinquent Rate | **6.06%** |

### 📆 Week-Over-Week (WoW) Changes

| Metric | Change |
|---|---|
| 📈 Revenue Growth | **+28.8%** |
| 🔄 Transaction Amount | Increased |
| 👥 Customer Count | Increased |

---

## ✨ Features

| Feature | Description |
|---|---|
| 🖥️ **Interactive Dashboard** | Fully interactive Power BI visuals with filters, slicers, and drill-throughs |
| ⚡ **Real-Time Insights** | Connected to live SQL data for up-to-date reporting |
| 🧮 **Advanced DAX Measures** | Custom DAX formulas for revenue, segmentation, and WoW calculations |
| 👥 **Customer Segmentation** | Age group and income group classification for demographic analysis |
| 🌍 **Geographic Analysis** | State-level revenue breakdown across the US |
| 📉 **Risk Monitoring** | Delinquency and activation rate tracking for risk assessment |
| 📊 **Revenue Attribution** | Breakdown by card category, gender, and transaction type |

---

## 🗄️ Data Sources

```
📦 SQL Database
 ├── 📄 public.cust_detail   → Customer demographic & profile data
 └── 📄 public.cc_detail     → Credit card transaction & financial data
```

The data pipeline involves:
1. **Data Ingestion** — Raw data loaded into a PostgreSQL database
2. **Data Transformation** — Cleaned and structured using SQL queries
3. **Data Modeling** — Relationships built in Power BI data model
4. **DAX Calculations** — Custom measures for business KPIs

---

## 🧮 DAX Queries

### 👥 Customer Segmentation

```dax
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
```

### 📅 Time Intelligence

```dax
week_num2 = WEEKNUM('public cc_detail'[week_start_date])
```

### 💰 Revenue Measures

```dax
Revenue = 
    'public cc_detail'[annual_fees] 
    + 'public cc_detail'[total_trans_amt] 
    + 'public cc_detail'[interest_earned]

Current_week_Revenue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
    )
)

Previous_week_Revenue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2]) - 1
    )
)
```

---

## 💡 Project Insights

### 🔄 Week-Over-Week Performance
- 📈 Revenue jumped by **28.8%** compared to the previous week
- 🔄 Transaction amounts and counts showed positive growth
- 👥 Customer engagement increased week-over-week

### 📆 Year-To-Date Highlights
- 💰 Total revenue reached **$57 Million**
- 🏦 Interest income contributed **$8 Million**
- 💳 Transaction volume totaled **$46 Million**
- 👨‍💼 Male customers drove **54%** of revenue ($31M vs $26M female)
- 💳 **Blue & Silver cards** dominate with **93%** of all transactions
- 🗺️ **Texas, New York & California** account for **68%** of total revenue
- ✅ Card activation rate stands at **57.5%**
- ⚠️ Delinquency rate tracked at **6.06%** — a key risk indicator

---

## 🛠️ Tech Stack

<div align="center">

| Technology | Purpose |
|---|---|
| ![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?logo=powerbi&logoColor=black) | Dashboard & Visualization |
| ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4479A1?logo=postgresql&logoColor=white) | Data Storage & Querying |
| ![DAX](https://img.shields.io/badge/DAX-E03A3E?logo=microsoft&logoColor=white) | Business Metrics & KPI Calculations |
| ![SQL](https://img.shields.io/badge/SQL-CC2927?logo=microsoftsqlserver&logoColor=white) | Data Transformation |

</div>

---

## 👤 Author

<div align="center">

**ABDELAALI ENNAMAT**

[![GitHub](https://img.shields.io/badge/GitHub-ABDELAALI--ENNAMAT-181717?style=for-the-badge&logo=github)](https://github.com/ABDELAALI-ENNAMAT)

_Data Analyst | Business Intelligence | Power BI Developer_

</div>

---

<div align="center">

⭐ **If you found this project useful, please consider giving it a star!** ⭐

</div>
