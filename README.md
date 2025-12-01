Vintage Haven – RFM Segmentation Analysis  
Looker Studio Dashboard: https://lookerstudio.google.com/reporting/92f2c237-6ef2-44f3-849e-93c0e4171fea

### Customer Value, Behaviour, and Marketing Prioritisation for a Growing Online Retailer

## 📋 Table of Contents
1. [Project Overview](#1-project-overview)  
2. [Business Context](#2-business-context)  
3. [Data Source](#3-data-source)  
4. [Data Overview](#4-data-overview)  
5. [Data Quality Considerations](#5-data-quality-considerations)  
6. [Methodology](#6-methodology)  
   - [Customer Typing](#61-customer-typing)  
   - [RFM Calculation](#62-rfm-calculation)  
   - [RFM Segmentation](#63-rfm-segmentation)  
   - [Dashboard](#64-dashboard)  
7. [Key Insights](#7-key-insights)  
8. [Marketing Recommendations](#8-marketing-recommendations)  
9. [Business Impact](#9-business-impact)  
10. [Tools & Skills Demonstrated](#10-tools--skills-demonstrated)  
11. [Repository Structure](#11-repository-structure)  
12. [Next Steps](#12-next-steps)


## 1. Project Overview
This project provides an end-to-end customer analytics solution for **The Vintage Haven**, a London-based retailer that expanded into an international online store.  

Using **RFM segmentation**, it analyses over **540,000 transactions** from the UCI Online Retail dataset to identify:

- High-value customers  
- Customers at risk of churn  
- Behaviour patterns across retail, small B2B, and wholesale buyers  
- The most efficient target groups for upcoming marketing campaigns  

The outputs include RFM scoring, segmentation logic, and an interactive dashboard created in Looker Studio.


## 2. Business Context
The Vintage Haven serves a diverse audience:

- Individual retail shoppers  
- Small B2B buyers  
- Wholesalers placing bulk orders  

These groups behave differently, which makes it difficult to understand who drives long-term value and where the marketing budget should be focused.

This project aims to:

- Identify the **most and least valuable** customer segments  
- Detect **behavioural patterns** and **early signs of churn**  
- Compare **retail vs business buyers**  
- Support a **data-driven marketing strategy** that maximises revenue


## 3. Data Source
- **Dataset:** Online Retail  
- **Author:** Chen, D. (2015)  
- **Repository:** UCI Machine Learning Repository  
- **DOI:** https://doi.org/10.24432/C5BW33  
- **Granularity:** Each row is a product-level line item on an invoice  


## 4. Data Overview

| Column      | Description                                      |
|------------|--------------------------------------------------|
| InvoiceNo  | Unique invoice ID (cancellations start with "C") |
| StockCode  | Product SKU                                      |
| Description| Product name                                     |
| Quantity   | Units purchased (negative = return)              |
| InvoiceDate| Date and time of transaction                     |
| UnitPrice  | Price per item in GBP                            |
| CustomerID | Unique customer identifier                       |
| Country    | Customer location                                |

### Coverage
- **Transactions:** 541,909  
- **Period:** December 2010 – December 2011  
- **Countries:** UK + international  
- **Unique products:** ~3,600 after cleaning and deduplication  


## 5. Data Quality Considerations
The raw dataset contained several quality issues:

- Missing **CustomerID** values (~25% of rows)  
- Negative quantities representing returns  
- Cancelled invoices (prefixed InvoiceNo)  
- Duplicate rows  
- Inconsistent product descriptions  
- Extreme outliers in quantity and unit price  

### Cleaning Actions
- Removed rows with missing CustomerIDs  
- Excluded cancelled invoices and duplicate rows  
- Standardised product descriptions to reduce duplication  
- Created new fields:  
  - `TotalPrice` (Quantity × UnitPrice)  
  - `Customer Type` (Individual / Small B2B / Wholesaler)  
  - RFM metrics: `Recency`, `Frequency`, `Monetary`  
- Retained outliers due to lack of external validation


## 6. Methodology

### 6.1 Customer Typing
Customers were classified based on **average quantity per order**:

- **Individuals:** \< 20 units  
- **Small B2B:** 20–100 units  
- **Wholesalers:** \> 100 units  

This grouping was used mainly for interpretation and fairness in scoring, not as the primary segmentation method.


### 6.2 RFM Calculation
For each customer:

| Metric   | Definition                           |
|----------|--------------------------------------|
| Recency  | Days since most recent purchase      |
| Frequency| Number of unique invoices            |
| Monetary | Total spending across all invoices   |

RFM values were derived from the cleaned transactional data.  

Scores from **1 to 5** were then assigned to each metric **within customer type** to avoid wholesalers dominating the scale due to high volumes.


### 6.3 RFM Segmentation
Based on R, F, and M scores, customers were assigned into the following segments:

- **Champions**  
- **Loyal**  
- **Potential Loyalists**  
- **Recent Customers**  
- **At Risk but Valuable**  
- **At Risk / Lost**  
- **Others**  

These segments form the basis for marketing prioritisation.


### 6.4 Dashboard
A Looker Studio dashboard was developed to:

- Visualise segment sizes by customer count  
- Compare behavioural patterns (Recency, Frequency, Monetary)  
- Analyse revenue concentration (Pareto view)  
- Compare customer types (Individual, Small B2B, Wholesaler) by revenue and volume  
- Support decision-making for future marketing campaigns  

> You can add the dashboard link here once published.


## 7. Key Insights

### 7.1 Revenue Concentration
- **Champions, Potential Loyalists, and At Risk but Valuable account for over 80% of total revenue.**  
- Remaining segments (Loyal, Others, At Risk/Lost, Recent Customers) represent nearly half of the customer base but only ~20% of revenue.

### 7.2 Engagement and Churn
- Over **30%** of customers are classified as **At Risk / Lost** or **At Risk but Valuable**, indicating a sizeable portion of previously active customers who have stopped buying.  
- **Recent Customers** make up **less than 5%**, suggesting limited new-customer acquisition relative to the volume of churn.

### 7.3 Customer Type Behaviour
- **Individuals** generate the highest total revenue, driven largely by their count.  
- **Small B2B customers** are the most **revenue-efficient**, generating almost 3× more revenue per customer than Individuals.  
- **Wholesalers** contribute high order values but are few and show more volatile behaviour.

### 7.4 Priority Segments
The analysis identifies three core priority segments:

- **Champions** – stable, high-value customers  
- **Potential Loyalists** – strong growth potential  
- **At Risk but Valuable** – high-value lapsed buyers with reactivation upside  


## 8. Marketing Recommendations

### 8.1 Champions – Retain
- Provide early access to new collections  
- Offer exclusive bundles or limited-edition items  
- Send appreciation-driven communications to maintain loyalty  

### 8.2 Potential Loyalists – Grow
- Use follow-up emails and product recommendations  
- Encourage second/third purchases with small incentives  
- Introduce loyalty or points-based benefits to build repeat behaviour  

### 8.3 At Risk but Valuable – Reactivate
- Run targeted win-back campaigns (“We miss you” + incentive)  
- Highlight new or relevant products based on past purchases  
- Use time-limited offers to prompt re-engagement  

### 8.4 Small B2B – High-ROI Focus
- Build reorder reminders and curated assortments  
- Offer volume-based discounts or business bundles  
- Prioritise them as a key audience for retention campaigns  

### 8.5 Lower-Priority Groups
- **At Risk / Lost** and **Others** should receive light-touch, automated communication (newsletters, seasonal campaigns) rather than high-spend efforts.  
- **Recent Customers** should be nurtured with onboarding flows and post-purchase follow-ups.


## 9. Business Impact
This RFM segmentation enables The Vintage Haven to:

- Allocate marketing budget toward customers with the highest potential return  
- Protect its most valuable relationships (Champions)  
- Grow promising segments (Potential Loyalists)  
- Reactivate high-value customers who have lapsed (At Risk but Valuable)  
- Understand the different roles of Individuals, Small B2B, and Wholesalers in overall revenue  

Overall, the project provides a clear, data-driven basis for the **next marketing campaign** and for ongoing customer management.


## 10. Tools & Skills Demonstrated
- **Python** (pandas, numpy) for data cleaning and transformation  
- **Exploratory Data Analysis (EDA)**  
- **RFM analysis and customer segmentation**  
- **Feature engineering** (TotalPrice, Customer Type, R/F/M metrics)  
- **Looker Studio** for dashboard design and storytelling  
- **Business and marketing analytics**  
- **Communicating findings to non-technical stakeholders**


