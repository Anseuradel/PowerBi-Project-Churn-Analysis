# PowerBi-Project Churn Analysis

<div align="center">
  <img src="https://github.com/Anseuradel/PowerBi-Project-Churn-Analysis/blob/main/assets/images/Telecom-company-powerbi-project-churn-analysis-image.webp" alt="Churn Analysis Dashboard" width="700"/>
  
  <h3> Interactive Business Intelligence Dashboard for Churn Analytics </h3>
  
  <img src="https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black" alt="Power BI"/>
  <img src="https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white" alt="Excel"/>
  <img src="https://img.shields.io/badge/Dashboard-FF6B6B?style=for-the-badge&logo=tableau&logoColor=white" alt="Dashboard"/>
</div>

---

# Project Overview 
## Objective : 

The goal of this project is to learn and apply data analysis using Power BI, one of the most widely used business intelligence tools in modern organizations. Power BI offers powerful capabilities for:

- Data cleaning and transformation

- Data modeling

- Interactive visualization

- Business-focused storytelling

Mastering Power BI is a strong asset for any data analyst, as it allows you to communicate complex insights in a clear, interactive, and professional way.
This project also serves as a demonstration of my analytical skills to recruiters, data professionals, and anyone interested in data-driven decision making.

## Data Source : 

The dataset used is the IBM Telco Customer Churn Dataset, which contains information about 7,043 fictional telecom customers in California during Q3.

It includes:

- Customer demographics

- Subscription information

- Services used (Internet, Phone, Streaming, etc.)

- Billing & charges

- Customer Lifetime Value (CLTV)

- Churn labels and churn scores

- Satisfaction ratings

I chose this dataset because customer churn is one of the most critical challenges for telecom companies. As customers, we often notice how aggressively telecom providers try to retain us when we attempt to cancel a subscription.
This project allowed me to step into the role of a telecom data analyst, uncovering churn patterns and providing actionable insights to improve retention.

Additionally, using a public IBM dataset avoids exposing any sensitive or proprietary company data.

## Technology : 

For this end-to-end project, I used:

- Power BI → data understanding, cleaning, modeling, DAX measures, and dashboard design

- Power Query → data transformation

- Figma → creation of a clean, modern dashboard layout and UI components

- GitHub → version control and project documentation

## Impact : 

This project aims to:

- Strengthen my practical skills in data analysis and business intelligence

- Build a professional portfolio piece

- Provide clear, data-driven insights to reduce customer churn

- Identify customer behaviors, risk factors, and retention opportunities

By combining strong analytics with thoughtful UI design, this project demonstrates both technical and storytelling skills—essential for successful BI and data analytics work.

---

# Problem Statement

Telecom companies face a major challenge: customer churn. Acquiring new customers is significantly more expensive than retaining existing ones.
Understanding who churns, why they churn, and how to prevent it is essential for profitability.

This project answers the following key business questions:

1. What is the overall churn rate?

2. Which customer segments are most likely to churn?

3. How do services, contracts, charges, and satisfaction levels influence churn?

4. Which geographic areas show higher churn risk?

5. How can the company prioritize high-value customers at risk?

The goal is to provide clear, actionable insights to guide retention strategy, customer experience improvements, and revenue protection.

# Data Modeling

To support efficient analysis, I designed a clean Star Schema with one Fact table and four Dimensional tables.

## Fact Table
FactCustomerStatus

Contains quarterly status information, churn labels, churn scores, CLTV, satisfaction, and all service/billing metrics merged from Services.

## Dimension Tables
| Dimension Table |	Description	| Key |
| -------------------- | -------------------------------------------------- |----|
| DimCustomerDemographics |	Age, gender, dependents, senior status | CustomerID |
| DimLocation	| City, State, Zip Code, coordinates	| CustomerID |
| DimZipPopulation |	Population per ZIP Code	| ZipCode |

## Relationships

DimCustomerDemographics (1) → (∞) FactCustomerStatus

DimLocation (1) → (∞) FactCustomerStatus

DimZipPopulation (1) → (∞) DimLocation

DimDate (1) → (∞) FactCustomerStatus

This model enables:

✔ clean slicing of churn metrics
✔ accurate filtering across demographics, geography, and services
✔ simplified DAX implementation

# Key DAX Measures
## Core Metrics

```DAX
Total Customers = COUNTROWS(FactCustomerStatus)

Churned Customers = CALCULATE(
    COUNTROWS(FactCustomerStatus),
    FactCustomerStatus[Churn Value] = 1
)

Churn Rate = DIVIDE([Churned Customers], [Total Customers])

Average Monthly Revenue = AVERAGE(FactCustomerStatus[Monthly Charge])

Total Revenue = SUM(FactCustomerStatus[Total Revenue])
```

## Customer Value & Risk

```DAX
Average CLTV = AVERAGE(FactCustomerStatus[CLTV])

High Risk Customers = CALCULATE(
    COUNTROWS(FactCustomerStatus),
    FactCustomerStatus[Churn Score] >= 60
)
```

