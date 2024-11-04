# LITA-CAPSTONE-PROJECT
This is where I documented my  captone project with the Incubator Hub 
## Project Title: Customer Data Analysis

### Project Overview
This data analysis project aims to analyze and generate insight into the customer data for a subscription service to identify key trends in cancellations and renewals. By analyzing the various parameters in the data received, i gathered enough insight into the problems and proferred the best possible solutions through compelling stories.

### Data Sources
The Primary source of data here is Customer Data.csv

### Data Collected
The data set includes the following key columns
1. customerID
2. customer name
3. region
4. subscription type
5. subscription start
6. subscription end
7. canceled
8. revenue

### Project Objectives.
This Project was designed to address the foloowing
1. Understand the reasons behind the high cancellation rate (41K out of 75K customers canceled), especially with the significant drop-off after 12 months.
2. Examine customer preferences across Basic, Premium, and Standard subscription types to determine which offerings generate the most interest and revenue.
3. Analyze customer distribution and cancellation rates across regions (North, East, South, and West) to identify any regional variations in customer behavior.
4. Track monthly customer activity and cancellations to identify seasonal trends or specific months with high activity or high cancellation rates (e.g., peak cancellations in April).
5. Investigate the average subscription duration across different plans

### Tools Used
This data was worked on using:
- Ms.Excel for data cleaning and data analysis, using the pivot tables to organize and summarize.
- SQL(structured Query Language) for data querying, to ensure the integrity and quality of data#
- PowerBi for data visualization, to represent the key insights visually.

### Data Cleaning and Preparation
- Data loading and inspection
- Data cleaning
- Removal of duplicates

### Exploratory Data Analysis
The EDA involved was focused on answering the follwowing questions:
- what is the total number of customers from each region.
- what is the most popular subscription type by the number of customers.
- customers who canceled their subscription within 6 months.
- what is the average subscription duration for all customers.
- customers with subscriptions longer than 12 months.
- what is the total revenue by subscription type.
- what are the top 3 regions by subscription cancellations.
- what is the total number of active and canceled subscriptions.

### Data Analysis
This shows and includes the formulars, basic lines of codes used and DAX expressions used during the analysis.

#### SQL for customer insights.
```SQL
SELECT *
FROM [dbo].[Customer Data]
---Q1 Retrieve the total number of customers from each region.---
SELECT Region, COUNT(CustomerID) AS Total_No_of_Customers
FROM [dbo].[Customer Data]
GROUP BY Region
--Q2 Find the most popular subscription type by the number of customers.
SELECT SubscriptionType,COUNT(CustomerID)AS NO_Of_Customers
FROM [dbo].[Customer Data]
GROUP BY SubscriptionType
--Q3 Find customers who canceled their subscription within 6 months
SELECT CustomerName,Canceled,SubscriptionStart
FROM [dbo].[Customer Data]
WHERE Canceled =0 AND MONTH(SubscriptionStart) BETWEEN 1 AND 6
--Q4 Calculate the average subscription duration for all customers
SELECT Count(CustomerID) As
All_Customers,AVG(DATEDIFF(DAY,SubscriptionStart,SubscriptionEnd)) AS
Average_Subscription_Duration
FROM [dbo].[Customer Data]
WHERE SubscriptionEnd IS NOT NULL
----Q5 Find customers with subscriptions longer than 12 months.DATEDIFF
SELECT CustomerName,SubscriptionType,SubscriptionStart,SubscriptionEnd
FROM [dbo].[Customer Data]
WHERE DATEDIFF(MONTH,SubscriptionStart,SubscriptionEnd) >=12
--- Q6 calculate total revenue by subscription type
SELECT SubscriptionType,SUM(Revenue) AS Total_Revenue
FROM[dbo].[Customer Data]
GROUP BY SubscriptionType
---Q7 Find the top 3 regions by subscription cancellations.
SELECT TOP 3 Region,Canceled
FROM [dbo].[Customer Data]
--Q8 Find the total number of active and canceled subscriptions.
SELECT
SUM( CASE WHEN Canceled = 0 THEN 1 ELSE 0 END) AS ActiveSubscriptions,
SUM (CASE WHEN Canceled = 1 THEN 1 ELSE 0 END) AS CanceledSubscriptions
FROM [dbo].[Customer Data]
GROUP BY CustomerID
```

#### -DAX functions with powerBi for conditional columns, calculated and measures
past out the dax function from the formular box

### DATA VISUALIZATIONS.
put in the screenshot of powerbi and pivot tables.

### FINAL ANALYSIS OUTCOME.
**1. 





