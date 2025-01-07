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
To access the dataset, click [**here**](https://github.com/Rolakamin/Maven-Toys-Sales-Performance/tree/main/Maven%20Toys%20Dataset).

## Data Cleaning and Transformation

These steps were taken to clean and transform the dataset, ensuring its accuracy, consistency, and readiness for analysis:

1. **Changing Data Types**
- The IDs in each table were converted from a whole number to text data type to prevent them from being misinterpreted as fields for aggregation. As identifiers, these fields are not intended for calculations.

2. **Trimming Text Fields**
- Text columns across the dataset were trimmed to remove unnecessary spaces, ensuring clean and consistent values.

3. **Standardizing Store Names**
- In the Stores table, the store names were standardized to create easy-to-read names. Originally, each row included "Maven Toys" at the beginning of the store name.
- The Replace Value function was used to replace "Maven Toys" with an empty string, resulting in explicit and concise store names for all rows.

4. **Creating Calculated Columns in the Sales Table**
- The Sales table, which serves as the fact table (containing all occurrences of transactions), required additional calculated columns: Profit, Total Cost, and Total Price.
- These calculations were made by merging data from the Products table into the Sales table using the Merge Queries function to bring in the relevant product cost and price.

5. **Profit and Cost Calculations**
- Calculations for the new columns were as follows:
  - **Total Cost**: Units Sold × Product Cost
  - **Total Price**: Units Sold × Product Price
  - **Profit**: Total Price − Total Cost
 
**Below are the screenshots showing the formulae used to calculate these columns:**
    
### Profit Calculation


![Profit Calculation](https://github.com/Rolakamin/Maven-Toys-Sales-Performance/blob/main/Profit.png)


### Total Cost Calculation


![Total Cost Calculation](https://github.com/Rolakamin/Maven-Toys-Sales-Performance/blob/main/Total_Cost.png)


### Total Price Calculation


![Total Price Calculation](https://github.com/Rolakamin/Maven-Toys-Sales-Performance/blob/main/Total_Price.png)

**Note:**
In the provided screenshots, the column is labeled as "Units." For clarity and consistency, this column has been renamed to "Units Sold" in the final version of the dataset and dashboard. This adjustment was made to ensure that the column name more accurately reflects its content, representing the number of units sold per transaction.

## Data Modelling

Modeling in Data Analysis refers to the process of organizing and structuring data to establish meaningful relationships between different tables in a dataset or between different datasets, as the case may be.

A Fact Table is the central table in a star schema or snowflake schema that stores quantitative data (facts) for analysis. It contains measurable, numerical values, often aggregated, and represents transactional or event data in the dataset. Fact tables are linked to dimension tables through foreign keys.

A Dimension Table provides descriptive, textual, or categorical information about the entities in the fact table. These tables enrich the data by offering context and attributes to analyze and categorize facts.

For this Maven Toys Sales Performance analysis, the Sales Table serves as the Fact Table, surrounded by other tables (dimension tables: Stores, Inventory, Products, and Calendar tables), forming a star schema on a 1-to-many relationship.

The data model is shown below:

![Data Model](https://github.com/Rolakamin/Maven-Toys-Sales-Performance/blob/main/DataModel.png)

## Data Analysis and Visualization
The approach and techniques used to analyze the dataset and derive meaningful insights are described in this section. The Power BI dashboard developed to visualize the results is also included.

### Key Performance Indicators (KPIs)
KPIs were developed to track sales performance, profitability, and growth trends. These measures represent key metrics that reflect the overall performance and success of the business.
The following KPIs are displayed on the dashboard card visuals to represent the core metrics of the business's performance:

- **YTD Profit(Profit):** `TOTALYTD([Total Profit], Calendar_Table[Date])`  
  Aggregates profit for the year to date.
- **YTD Revenue(Revenue):** `TOTALYTD([Total Revenue], Calendar_Table[Date])`  
  Aggregates revenue for the year to date.
- **YTD Units Sold(Units Sold):** `TOTALYTD([Total Units Sold], Calendar_Table[Date])`  
  Aggregates units sold for the year to date.
- **Prev YTD Profit:** `CALCULATE([YTD Profit], SAMEPERIODLASTYEAR(Calendar_Table[Date]))`  
  Captures profit for the previous year to date.
- **Prev YTD Revenue:** `CALCULATE([YTD Revenue], SAMEPERIODLASTYEAR(Calendar_Table[Date]))`  
  Captures revenue for the previous year to date.
- **Prev YTD Units Sold:** `CALCULATE([YTD Units Sold], SAMEPERIODLASTYEAR(Calendar_Table[Date]))`  
  Captures units sold for the previous year to date.
- **YoY Revenue Growth:**  
  `DIVIDE([YTD Revenue] - [Prev YTD Revenue], [Prev YTD Revenue])`  
  Tracks yearly percentage growth in revenue.
- **YoY Profit Growth:**  
  `DIVIDE([YTD Profit] - [Prev YTD Profit], [Prev YTD Profit])`  
  Shows the yearly percentage growth in profit.
- **YoY Growth in Units Sold:**  
 `DIVIDE([YTD Units Sold] - [Prev YTD Units Sold], [Prev YTD Units Sold])`  
  Highlights year-over-year growth in product sales.
- **Revenue Target:** `8500000`  
  Sets the benchmark for revenue performance.
- **Progress Towards Target (YTD):**  
  `DIVIDE([YTD Revenue], [Revenue Target])`  
  Measures how much of the revenue target has been achieved so far.
- **Progress Towards Target (PYTD):**  
  `DIVIDE([Prev YTD Revenue], [Revenue Target])`  
  Evaluates progress toward last year’s target for comparison.
  
In addition to the KPIs displayed in the card visuals, the following measures were calculated and utilized for a deeper understanding of the business performance:

- **Total Profit:** `SUM(Sales[Profit])`  
  Indicates the overall profitability of sales.
- **Total Revenue:** `SUM(Sales[Total_Price])`  
  Reflects the total income generated from sales.
- **Total Units Sold:** `SUM(Sales[Units Sold])`  
  Represents the total quantity of products sold.
  
### Power BI Dashboard

The Power BI dashboard was designed to provide a detailed view of Maven Toys' sales performance. It highlights the KPIs, trends, and other visuals, offering insights into the business problems and helping to guide decision-making.

![Power BI Dashboard](https://github.com/Rolakamin/Maven-Toys-Sales-Performance/blob/main/Maven%20Toys%20Dashboard.png)  


[Explore the Dashboard here](#)

### Key Notes:
- YTD Revenue, YTD Profit, and YTD Units Sold represent the metrics on the card visuals as Revenue, Profit, and Units Sold respectively.
- Prev YTD values (for Profit, Revenue, and Units Sold) provide the comparison for the same period in the previous year.
- YoY Growth for each of the key metrics gives percentage changes over the year.
- Progress Towards Target compares actual performance against the set target.
