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

### Key Definitions
The following terms are essential for understanding the metrics used in the analysis. The definitions are provided in the context of the dataset, which spans from January 1, 2022, to September 30, 2023.

1. **YoY (Year-over-Year)**: Represents the percentage change in the aggregated performance of a metric for the year-to-date (YTD) in the current year compared to the previous year-to-date (PYTD).
- Example: YoY Revenue Growth compares total revenue from January 1, 2023, to September 30, 2023, with total revenue from January 1, 2022, to September 30, 2022, and calculates the percentage increase or 
              decrease.
2. **YTD (Year-to-Date)**: Refers to the cumulative performance of a metric from the start of the current year up until a specific date.  
- Example: Total revenue from January 1, 2023, to September 30, 2023.  
3. **PYTD (Previous Year-to-Date)**: Represents the cumulative performance from the start of the previous year up until the same date as YTD.  
- Example: Total revenue from January 1, 2022, to September 30, 2022.  
4. **SPLY (Same Period Last Year)**: Compares the performance of a specific period in the current year to the same period in the previous year, commonly used for months or quarters.  
- Example: Comparing Q3 2023 (July to September) to Q3 2022.

## Findings and Insights

**Year-over-Year (YoY) Growth Analysis**

Between January 1, 2023, and September 30, 2023, Maven Toys generated approximately $6.96 million in revenue, reflecting a 30.9% YoY growth compared to the $5.32 million made during the same period in 2022. Similarly, profit increased by 16%, rising from approximately $1.57 million in 2022 to $1.82 million in 2023. The total units sold also experienced significant growth, increasing by 40.8% from 384,415 units in 2022 to 541,073 units in 2023. Overall, between January 2022 and September 2023, Maven Toys generated $14.44 million in revenue, $4.01 million in profit, and sold 1.09 million units in total.

**Progress Toward Revenue Targets**

Maven Toys set a revenue target of $8.5 million for both 2022 and 2023. By the end of September 2023, progress to this target was 81.9% (approximately $6.96 million). This represents a notable improvement compared to the same period in 2022, when progress to target stood at 62.6%. By the end of December 2022, Maven Toys achieved 88.03% of the annual target (approximately $7.48 million), but the target was not met. Given the holiday season from October to December, revenue is expected to increase significantly, suggesting that the 2023 target is more likely to be met.

**Product Category Profitability**

For the Year-to-Date (YTD) period of 2023, the Toys category drove the highest profit, contributing $257.77k, followed closely by Electronics, which generated $233.25k. However, profitability varied by store location. For example:
- At Airport locations, Games ($30.32k) and Toys ($25.25k) were the top profit contributors.
- At Commercial locations, Electronics ($68.02k) and Toys ($51.63k) performed best.
- At Downtown locations, Toys ($150.02k) and Arts and Crafts ($148.83k) led in profitability
- At Residential locations, Arts and Crafts ($32.26k) and Toys ($30.89k) topped the chart.
While Toys and Electronics consistently contributed the highest profits overall, this trend was not uniform across all locations.

**Store Locations: Revenue and Profit Performance**

Downtown locations generated the highest revenue ($3,992k or 57% of the total) and the highest profit ($1,030.82k) during the YTD period. This was followed by Commercial locations, which brought in $1,552k in revenue (22%) and $408.97k in profit. Airport locations contributed the least, with $639k in revenue and $173.04k in profit, followed by Residential locations with $778k in revenue (11%) and $211.42k in profit.

**Seasonal Trends and Patterns**

In 2022, the month of December generated the highest revenue ($877,204), followed by April ($681,073). These months align with periods of high tourist activity and major festive seasons in Mexico, such as Christmas and Easter, which encourage gift-giving and drive higher sales.

In 2023, March emerged as the month with the highest revenue ($883,516). March is a busy tourist season in Mexico, which likely contributed to increased sales during this time. However, in 2022, despite being part of the tourist season, March did not perform as strongly, generating $589,485 in revenue. This was lower than other months like April, May, and June, suggesting that additional factors such as promotional campaigns, product availability, or economic conditions may have influenced sales during this period.

A recurring dip in revenue was observed in August for both years. In August 2022, revenue stood at $489,423, while in August 2023, it increased to $660,877. This dip is likely tied to the school calendar in Mexico, which runs from late August to early July. Parents tend to prioritize spending on back-to-school supplies and clothing during this period, leading to reduced expenditure on toys.

In terms of total units sold, December 2022 recorded the highest sales (66,031 units), followed by November (51,185 units). This surge in sales can be attributed to holiday shopping activities. On the other hand, February and August recorded the lowest total units sold in 2022, with February at 36,935 units and August at 39,927 units.

In 2023, March saw the highest total units sold (69,336 units), reflecting a peak in demand early in the year. This was followed by July, which recorded 63,614 units sold. However, the lowest total units sold occurred in August (51,193 units), followed by September (52,152 units) and February (54,581 units).

Both years showed a noticeable dip in February, despite an improvement in units sold year-over-year. The consistent dip in August across both years highlights a recurring trend of reduced demand during this period.

**Top Performing Products and Stores**

The analysis revealed that the top five products by profit were Colourbuds, Lego Bricks, Action Figures, Barrel O’Slimes, and Deck of Cards, indicating strong consumer demand and profitability for these items.

In terms of store performance, Ciudad de Mexico 2, Guadalajara, Toluca 1, Ciudad de Mexico, and Monterrey 2 emerged as the top-performing cities by revenue, while the highest profits were recorded in Ciudad de Mexico, Guadalajara, Monterrey, Hermosillo, and Guanajuato. Conversely, cities like Merida, La Paz, Cuernavaca, Aguascalientes, and Oaxaca reported the lowest profits.

While the exact reasons for low profits in some cities remain unclear, potential contributing factors could include economic conditions, population size, or consumer preferences. However, the lack of demographic and socioeconomic data limits a deeper understanding of these trends.

## RECOMMENDATIONS

1. **Focus on High-Performing Areas**

- Prioritize opening stores in downtown/urban centers of new cities, as they consistently yield the highest revenue and profit due to strong demand and spending power.
- Target commercial hubs with heavy foot traffic, similar to the successful performance in current commercial locations.
  
2. **Address Low-Performing Cities**

- Investigate underperforming cities like Merida, La Paz, Cuernavaca, Aguascalientes, and Oaxaca to identify causes such as low population density, income levels, or weak marketing.
- If market potential remains insufficient, consider consolidating or closing operations in these cities.
  
3. **Capitalize on Seasonal Trends**

- Increase marketing and promotional efforts ahead of high-revenue months like December, March, and April.
- Stock high-demand products like Colourbuds, Lego Bricks, and Action Figures well in advance of festive and tourist seasons.
- Open stores in tourist-heavy cities and cultural hubs to boost seasonal revenue.
  
4. **Optimize Product Offerings by Location**

Tailor inventory to location-specific preferences:For example,

- **Airport locations**: Focus on games and toys targeting travelers.
- **Residential areas**: Prioritize arts and crafts and toys to cater to families and children.
  
5. **Leverage Best-Selling Products**

- Ensure consistent availability of best-sellers (e.g., Colourbuds, Lego Bricks, Action Figures) across all locations.
- Implement promotions to stabilize sales during February and August, which historically show dips in revenue.
  
6. **Test New Markets Strategically**

- Pilot ‘pop-up stores,’ ‘play areas,’ or online sales campaigns in potential new markets to gauge demand before committing to permanent locations.
  
7. **Leverage Data for Expansion**

- Use demographic, economic, and consumer spending data to identify untapped cities that share characteristics with high-performing locations like Ciudad de Mexico and Guadalajara.
  
8. **Expand E-Commerce Reach**

- Invest in online sales channels to serve regions with lower profitability, minimizing the need for physical store investments while maintaining market presence.

By following these strategies, Maven Toys can effectively target high-potential locations, optimize resources, and achieve sustainable growth.

## CHALLENGES AND LIMITATIONS

- **Data Availability and Quality**: Some data points, such as demographic and socioeconomic information for underperforming locations, were not available, limiting deeper insights into consumer behavior.
- **Short Timeframe**: The analysis covered only two years, which might not capture longer-term trends or anomalies.
- **Subjectivity in Interpretation**: Insights and recommendations are based on trends observed in the provided data and may not fully align with on-ground realities.
- **Seasonal Bias**: Months with high revenue, such as December and March, might mask other factors influencing performance during slower periods.

## REFERENCES

**How to create a CALENDAR TABLE in PowerBI using DAX**: https://youtu.be/b23bk6TcXak?si=B-ALBOUX1K9F2Yrh

**Data Modelling in PowerBI** :https://youtu.be/4ePNrdxWtY0?si=VvPHqf1ZVBKjfQo_

