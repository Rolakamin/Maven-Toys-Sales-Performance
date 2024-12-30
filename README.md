# Maven Toys Sales Performance Analysis

![](https://github.com/Rolakamin/Maven-Toys-Sales-Performance/blob/main/toys%20shop.png)
---

## Introduction

**Maven Toys**, a fictional chain of toy stores in Mexico, is planning to expand its business by opening new stores. To support this effort, I was hired as a Business Intelligence (BI) consultant to analyze their sales and inventory data, uncover patterns and trends, and provide actionable insights for informed decision-making.

Using data from January 2022 to September 2023, I evaluated key performance indicators (KPIs) such as revenue, profit, and units sold, alongside trends in monthly revenue and units sold over time, as well as product and store performance. With an annual revenue target of $8.5 million for both 2022 and 2023, the project focuses on assessing the company’s progress toward these goals while identifying top-performing and underperforming stores and locations.

To present these insights effectively, I developed a single-page interactive dashboard in Power BI, enabling stakeholders to make data-driven decisions and shape their expansion strategy.

## Project Overview 

Maven Toys, a fictional chain of toy stores in Mexico, seeks to expand its operations by opening new stores. An analysis of sales and inventory data from January 2022 to September 2023 provides key insights into patterns and trends, which will guide the company's expansion strategy.

### Business Objectives

The main objective of Maven Toys is to expand its business by opening new stores. To make informed decisions about where to open new locations, the company relies on data-driven insights derived from sales and inventory data.

### Business Problems

To achieve its expansion goals, Maven Toys needs to address the following key questions:

•	What is the Year-over-Year (YoY) growth in revenue, profit, and units sold? How did Maven Toys perform in the previous year?

•	Maven Toys has set a target of $8.5 million in revenue for each year — 2022 and 2023. How much progress has been made toward this goal by evaluating Year-to-Date (YTD) and Previous-Year-to-Date (PYTD) growth?

•	Which product categories drive the biggest profits? Is this consistent across store locations?

•	Which store locations have the highest potential for profitability?

•	Can seasonal trends or patterns in sales data be identified that might affect the timing and location of new store openings?

•	Which stores are top performers in terms of revenue and profit?

## Dataset Overview

### Dataset Details
The dataset provided for this analysis consists of six tables in CSV format:

1.	**Products Table**: Contains 35 products sold at Maven Toys. Each record represents a product, with details about the product category, cost, and retail price.
2.	**Stores Table**: Contains 50 Maven Toys store locations. Each record represents one store, with fields detailing the location, type, and opening date.
3.	**Sales Table**: Contains over 800,000 sales transactions (January 2022 – September 2023). Each record represents a purchase of a specific product at a specific store on a specific date.
4.	**Inventory Table**: Contains over 1,500 records representing the stock on hand for each product at each store as of October 1, 2023.
5.	**Calendar Table**: A single-column table listing dates from January 1, 2022, to September 30, 2023.
6.	**Data Dictionary**: Provides detailed descriptions for each field in the dataset, ensuring clarity and proper usage.

### Data Sources
The dataset includes the following files:
•	inventory.csv (1,593 rows, 3 columns)
•	products.csv (35 rows, 5 columns)
•	sales.csv (829,262 rows, 5 columns)
•	stores.csv (50 rows, 5 columns)

Although the calendar.csv file was part of the dataset, I opted to generate a new calendar table in Power BI using the **CALENDAR** function to:
1.	Avoid unnecessary dates and hidden fields that would have been included if i had use CALENDARAUTO.
2.	Align the exact date range with the provided dataset (January 2022 – September 2023).
3.	Dynamically create time-based columns such as Year, Month, Month Number, Quarter for enhanced flexibility and easier maintenance of the data model
   
The **DAX formulas** used to create the calendar table and its columns are provided below:

 **Date Range**:  
  `Calendar_Table(DATE(2022, 1, 1), DATE(2023, 9, 30))`

- **Year**:  
  `YEAR(Calendar_Table[Date])`

- **Month**:  
  `FORMAT(Calendar_Table[Date],"MMM")`

- **Month_Number**:  
  `MONTH(Calendar_Table[Date])`

- **Quarter**:  
  `"Q" & QUARTER(Calendar_Table[Date])`
  
### **Dataset Download Link**
To access the dataset, click [**here**](https://github.com/Rolakamin/Maven-Toys-Sales-Performance/tree/main/Dataset).


