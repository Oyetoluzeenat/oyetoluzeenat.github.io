---
layout: post
title: "EHub Sales Analysis: Revenue, Profitability, and Regional Performance"
date: 2025-06-16
categories: [Data Analytics, Business Intelligence, Healthcare]
tags: [Python, Power BI, Sales Analysis, Data Visualization, Healthcare Analytics]
author: Your Name
permalink: /portfolio/ehub-sales-analysis/
author: "Oyetolu Zeenat"

---
[Back to Portfolio Website](https://oyetoluzeenat.github.io/)
[**View the Full Codebase on GitHub**](https://github.com/Oyetoluzeenat/ehub-sales-analysis)
---

# eHub Sales Analysis: Revenue, Profitability, and Regional Performance

## Introduction

Data-driven decision-making is essential for healthcare distribution businesses operating in competitive markets. This analysis examines sales transactions from Drugstoc eHub to uncover trends in revenue generation, profitability, regional performance, product demand, and pricing effectiveness.

The project involved data cleaning, exploratory data analysis (EDA), visualization, and business intelligence reporting using industry-standard analytical techniques. The objective was to identify key performance drivers and provide actionable recommendations to improve revenue growth and profit margins.

---

## Dataset Overview

The dataset contains pharmaceutical sales transactions with the following fields:

| Field            | Description                                                             |
|------------------|-------------------------------------------------------------------------|
| Product_Name     | Name of the drug or product                                             |
| Product_Category | Product category (Antibiotics, Supplements, Vaccines, Analgesics, etc.) |
| Quantity_Sold    | Number of units sold                                                    |
| Unit_Price       | Selling price per unit (₦)                                              |
| Discount         | Discount applied (%)                                                    |
| Revenue          | Total sales value after discount                                        |
| Cost_Price       | Cost per unit (₦)                                                       |
| Profit           | Net profit from the transaction                                         |
| Payment_Term     | Cash, 30 Days, or 60 Days                                               |
| Sales_Rep        | Sales representative responsible for the sale                           |

---

## Data Cleaning and Preparation

Before conducting the analysis, the dataset was reviewed to ensure accuracy and consistency.

### 1. Data Quality Assessment
- Checked for missing values across all columns  
- Removed duplicate records  
- Corrected inconsistent categorical values  
- Standardized naming conventions  

### 2. Date Transformation
The `Invoice_Date` field was converted into a valid date format, and additional temporal features were derived:
- Month  
- Quarter  
- Year  

These enabled trend-based analysis over time.

### 3. Revenue Validation
A computed revenue metric was created:

**Computed Revenue = Quantity Sold × Unit Price × (1 − Discount/100)**

This was compared against recorded revenue. Transactions with discrepancies greater than 2% were flagged for review.

### 4. Outlier Detection
Profit and discount distributions were analyzed to detect anomalies that could distort insights. Extreme values were reviewed and handled appropriately.

---

## Exploratory Data Analysis

### Top Revenue-Generating Products

The analysis revealed that **Ceftriaxone 1g** was the top-performing product:

- ₦11.5M in revenue  
- 20.2% contribution to total sales  

Other key contributors included:
1. Ceftriaxone 1g  
2. Azithromycin 250mg  
3. Omeprazole 20mg  

---

### Product Category Profitability

While high-volume products drove revenue, **Analgesics** emerged as the most profitable category.

**Key insight:** High sales volume does not always translate to high profit margins.

---

### Regional Performance Analysis

| Region | Revenue | Contribution |
|--------|---------|--------------|
| South  | ₦20.5M  | 36.3%        |
| West   | ₦9.5M   | 16.4%        |

- **Best performing region:** South  
- **Lowest performing region:** West  

---

### Customer Segment Analysis

Customer groups (Pharmacies, Hospitals, Wholesalers) exhibited different purchasing behaviors and pricing sensitivities, significantly influencing profitability.

---

### Discount Impact on Profitability

A clear inverse relationship was observed between discounts and profit margins.

**Key insight:** Higher discounts consistently reduce profitability, despite potential short-term sales gains.

---

### Sales Representative Performance

Performance was evaluated using:
- Total revenue generated  
- Total profit generated  

This provides a framework for performance benchmarking and knowledge sharing across the sales team.

---

## Visualization Strategy

### Monthly Sales Trend
Sales peaked in February and declined steadily through September.

**Insight:** The business shows strong early-year momentum but weak mid-to-late year performance.

---

### Profit by Region
The South region significantly outperformed all others, while the West lagged behind.

---

### Product Category Performance
Analgesics dominated profitability across categories.

---

### Discount vs Profit Relationship
Scatter analysis confirmed that increased discounting reduces profit margins.

---

## Business Insights

### Sales Trends
- Strong Q1 performance  
- Continuous decline after February  
- Need for sustained demand strategies post-Q1  

### Best Performing Areas
**Products**
- Ceftriaxone 1g  
- Azithromycin 250mg  
- Omeprazole 20mg  

**Category**
- Analgesics  

**Region**
- South Region  

### Underperforming Areas
- Ibuprofen 400mg  
- Multivitamin Tablets  
- West Region  

---

## Recommendations

### 1. Strengthen the West Region
- Investigate distribution inefficiencies  
- Address pricing competitiveness  
- Improve product-market alignment  
- Increase targeted marketing  

---

### 2. Optimize Discount Strategy
- Introduce volume-based discounts  
- Reduce blanket discounting  
- Protect margins on premium products  

---

### 3. Improve Product Portfolio Management
- Reassess low-performing products  
- Consider discontinuation or repositioning  
- Bundle weak products with high-performing SKUs  

---

### 4. Protect High-Margin Products
Analyze success drivers of high-margin products like Vital Care and replicate strategies across other product lines.

---

## Power BI Dashboard Design

The executive dashboard includes:

### KPI Cards
- Total Revenue  
- Total Profit  
- Top Product  
- Best Region  

### Trend Analysis
- Monthly Sales Trend  
- Quarterly Performance  

### Regional Insights
- Revenue by Region  
- Profit by Region  

### Product Insights
- Top Products  
- Category Performance  

---

## Conclusion

This analysis highlights the importance of combining data cleaning, exploratory analysis, and business intelligence tools to drive strategic decision-making.

While Drugstoc eHub demonstrates strong performance in specific products and regions, opportunities exist in:
- Strengthening underperforming regions  
- Optimizing discount strategies  
- Improving portfolio efficiency  
- Enhancing margin protection  

Implementing these recommendations can support sustainable revenue growth and improved profitability.