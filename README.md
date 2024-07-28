# Drug Sales Dashboard

## Table of Content
  - [Project Overview](#project-overview)
  - [Data Sources](#Data-Sources)
  - [Tools](#tools)
  - [Data Cleaning/Preparation](#data-cleaning/preparation)
  - [Data Modelling](#data-modelling)
  - [Exploratory Data Analysis](#exploratory-data-analysis)
  - [Data Analysis](#data-analysis)
  - [Results Findings](#results-findings)
  - [Conclusion](#conclusion)
    
###  Project Overview
The objective of this project is to create a comprehensive and interactive dashboard to analyze drug sales data, providing key insights into sales performance, customer behavior, and product success.

<img width="623" alt="DRUG SALES DASHBOARD OPEN FILTER PAGE" src="https://github.com/user-attachments/assets/d341e15f-7264-4c84-b12d-76259cdd7bea">


### Data Sources
1. Fact Table: The Fact Table contains all the transactions of purchases made in the store. It includes detailed information on each transaction, providing a comprehensive dataset for analysis.
2. Drug Lookup Table: The Drug Lookup Table contains detailed information about each drug available in the store. 
3. Customer Table: The Customer Table contains detailed information about each customer who has made a purchase in the store

### Tools
- Power Query: Power Query will be used for data extraction, transformation, and loading (ETL)
- Power BI was used to create interactive and comprehensive dashboards.

### Data Cleaning/Preparation
- Remove Duplicates
- Handle Missing Values
- Standardize Data Types
- Validate Data Integrity
  
### Data Modelling
- Define Data Model
- Entity-Relationship Diagram (ERD)
- Create Tables and Relationships
- Create Calendar date
- Create Measures and Calculated Columns
- Optimize Model

### Exploratory Data Analysis
EDA involve exploring the sales data to answer key questions
1. Overall Sales Metrics
- Quantity sold, cost of goods sold (COGS), revenue, 
profit, and profit margin with comparing current month 
vs previous month
2. Performance of Top and Bottom Drugs:
- Identification of dynamic top drugs by Different 
Measures and the percentage contributions
- Overview of the Dynamic Top and underperforming
customers by Different Measures and the percentage
contribution

### Data Analysis
-  A Dynamic Measure for my drug sales dashboard was created.
    - This measure will change its calculation based on the selection from the slicer, allowing me to switch between different metrics such as total revenue, profit, quantity sold, and the number of transactions.
  
  ``` DAX FUNCTION
Dynamic Measure = 
    VAR _Dynamic_Measures =
        SELECTEDVALUE('Active Measure'[Active Measure Order])
        RETURN(
            SWITCH(
                TRUE(),
                _Dynamic_Measures=0,[Total Revenue],
                _Dynamic_Measures=1,[PROFIT],
                _Dynamic_Measures=2,[Quantity Sold],
                [#Transactions]))
```
- % Top Drugs
    -calculates the percentage of top drugs based on a dynamic measure such as revenue, profit, quantity sold, etc that was selected.
```DAX FUNCTION
% Top  Drugs = 
    DIVIDE(
    
            VAR _TopDrugs = 
            TOPN('Top/Bottom Drugs Value'[Top/Bottom Drugs Value Value],
            ALL(DrugLookup[DrugName]),[Dynamic Measure],DESC)

            VAR _ActiveDrug =
            SELECTEDVALUE(DrugLookup[DrugName],"All")

            VAR _TotalDynamicTopN =
                SUMX(_TopDrugs,[Dynamic Measure])

            RETURN 
                IF(
                    _ActiveDrug="All",
                    _TotalDynamicTopN,

                IF(
                    _ActiveDrug IN _TopDrugs,
                    [Dynamic Measure],
                    BLANK()

                )
                )
            ,[Dynamic Measure],0

            )
```

  ### Results Findings

1.  Overall Sales Metrics:

Track and compare key metrics such as quantity sold, cost of goods sold (COGS), revenue, profit, and profit margin for the current month vs. the previous month.

2. Performance of Top and Bottom Drugs:

- Top 5 Drugs Analysis:
  - The top 5 drugs generated 23.3% of the total revenue.
  - Deoxycline was the top-performing drug product with the highest revenue contribution.
  - Warafin had the least revenue contribution among the top 5 drugs, contributing only 0.3% of the total revenue.
- Customer Performance:
   - 24.4% of the total revenue came from the top 5 customers.
   - David Johnson was the most performing customer with the highest revenue contribution.
3. Sales Trends and Profit Margins:

- While sales in January generated the most revenue, the profit margins across different months were similar, indicating no significant difference in profitability throughout the year.

###  Conclusion

The drug sales dashboard offers a powerful tool for analyzing and visualizing sales data, providing stakeholders with crucial insights into overall sales performance, customer behavior, and product success. By focusing on key metrics such as revenue, profit, and profit margin, the dashboard enables users to:

- Identify top-performing and underperforming drugs and customers, allowing for targeted marketing and sales strategies.
- Compare sales performance across different time periods to recognize trends and make data-driven decisions.
- Optimize inventory management by understanding which products are in high demand and which are lagging.
- Improve customer satisfaction by identifying the most valuable customers and tailoring services to their needs.

With the top 5 drugs generating 23.3% of the revenue and the top 5 customers contributing 24.4% of the total revenue, the dashboard highlights the significance of these key players in the business. Furthermore, despite variations in monthly sales revenue, the consistent profit margins across months indicate stable profitability.

  
