# LITA-CAPSTONE-PROJECT(CUSTOMER DATA)
This is where I documented my Customer data captone project with the Incubator Hub 

## Project Title: Customer Data Analysis
---

### Project Overview

This data analysis project explored customer data to uncover trends in cancellations and renewals for a subscription service. The analysis revealed key insights into the underlying issues, informing data-driven recommendations for improvement.


---

### Data Sources
The Primary source of data here is Customer Data.csv

---

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
---

### Project Objectives.
This Project was designed to address the following
1. Understand the reasons behind the high cancellation rate (41K out of 75K customers canceled), especially with the significant drop-off after 12 months.
2. Examine customer preferences across Basic, Premium, and Standard subscription types to determine which offerings generate the most interest and revenue.
3. Analyze customer distribution and cancellation rates across regions (North, East, South, and West) to identify any regional variations in customer behavior.
4. Track monthly customer activity and cancellations to identify seasonal trends or specific months with high activity or high cancellation rates (e.g., peak cancellations in April).
5. Investigate the average subscription duration across different plans
---

### Tools Used
This data was worked on using:
- Ms.Excel for data cleaning and data analysis, using the pivot tables to organize and summarize.
- SQL(structured Query Language) for data querying, to ensure the integrity and quality of data#
- PowerBi for data visualization, to represent the key insights visually.
---

### Data Cleaning and Preparation
- Data loading and inspection
- Data cleaning
- Removal of duplicates
---

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

---

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
```DAX
Average subscription Duration = AVERAGE(CustomerData[Duration in Days])
count of Customer ID = COUNT(CustomerData[CustomerID])
Total Active = CALCULATE(COUNTROWS(CustomerData),'CustomerData'[No of cancelled]=0)
Total Cancelled = CALCULATE(COUNTROWS(CustomerData),'CustomerData'[No of cancelled]=1)
Table.AddColumn(#"Extracted Month Name", "second cancelations", each if [Canceled] = "true" then "Cancelled"
Table.AddColumn(#"Renamed Columns", "Cancellation 1 and 0", each if [Canceled] = true then 1 else 0)
```
---

### DATA VISUALIZATIONS.

![Screenshot (21)](https://github.com/user-attachments/assets/6b8c16ff-c5ae-4318-933b-2e5e40557ddf)



![Screenshot (20)](https://github.com/user-attachments/assets/a77f8e05-2c04-4b82-b55f-12dc62311c2f)

---



### FINAL ANALYSIS OUTCOME.
1. Problem Identification
2. Key Insights and Inferences
3. Recommendations

#### 1. Problem Identification
From the customer data, several key issues can be identified: 

##### High Cancellation Rate:
There’s a significant number of cancellations compared to active customers, with a noticeable peak in cancellations by month around April. 
##### Regional Cancellation Patterns:
Cancellations are relatively high across all regions, with each region contributing equally (North, South, and West each with 11,250 cancellations). 
##### Subscription Type Popularity and Revenue:
While the "Basic" subscription type is the most popular and brings in the most revenue, there’s a substantial gap between it and the Premium and Standard options. 
##### Subscription Duration Consistency:
The average duration across all subscription types (Basic, Premium, Standard) is consistently around 12 months, suggesting that most customers do not renew beyond the initial year. 

#### 2. Key Insights and Inferences
##### Customer Segmentation by Region:
Each region (North, East, South, and West) has around 18.75K customers, showing an even distribution across regions. This uniformity suggests a balanced customer base across locations but may mask regional preferences or differences in customer needs. 

#### Subscription Type Preferences:
- *Basic subscriptions* are the most popular, with around 38K subscribers, followed by Premium and Standard with approximately 19K each. This preference indicates a customer tendency toward more affordable options.
- *Revenue Contribution by Subscription Type:*
Basic subscriptions contribute the highest revenue at 75M, while Premium and Standard subscriptions add 38M and 37M, respectively. This suggests that customers are price-sensitive but willing to invest in basic services.

##### Customer Activity Trends:
- The "Total Active by Month" line graph reveals that customer engagement or activity fluctuates throughout the year, with peaks in certain months. Identifying these peak periods could help in targeting retention campaigns or introducing engagement incentives during off-peak times.
- A similar trend is observed in "Total Cancelled by Month," with a spike in cancellations around April. This might indicate a seasonal drop-off point where customers reassess or cancel their subscriptions, possibly after a trial period or due to seasonality. 

##### Cancellation Analysis:
- The pie chart shows that out of a total of 75K customers, 41K have canceled, while 34K remain active. This high cancellation rate (around 55%) raises concerns about customer retention and satisfaction.
- The "Top 3 Regions by Cancelled Subscription" chart indicates that cancellations are equally distributed across the North, South, and West regions, hinting that the issue might be tied to factors other than regional service discrepancies. 

##### Average Duration of Subscription:
- All subscription types have an average duration of 12 months, suggesting that customers are likely not renewing after the first year. This could indicate a lack of long-term value perceived by the customers or insufficient engagement strategies to retain them. 

#### 3. Recommendations 
##### Retention Strategies: 
- Given the high cancellation rate, especially around the 12-month mark, it’s crucial to implement a customer retention strategy. This could involve loyalty programs, personalized offers, or renewal discounts targeting customers approaching the 12-month end of their subscription.
- To address the April spike in cancellations, consider introducing engagement campaigns or perks in March to preempt potential drop-offs. 
##### Subscription Offering Improvements: 
- Since Basic subscriptions are the most popular, explore ways to add value to Premium and Standard subscriptions, possibly by offering exclusive features or discounts that might attract customers willing to upgrade. 
- Alternatively, a tiered Basic+ plan could be introduced to provide an intermediate option between Basic and Premium, catering to customers who want more features without the full Premium price. 
##### Regional Campaigns: 
- Although cancellations are evenly distributed across regions, targeting retention campaigns regionally could allow for more tailored solutions. Customer feedback surveys in each region may reveal specific pain points that can be addressed in marketing or service delivery. 
##### Customer Engagement Throughout the Year: 
- Use insights from the "Total Active by Month" data to schedule targeted engagement efforts during months of low activity, encouraging continuous use of the service. Educational content, seasonal promotions, or usage incentives can be useful to maintain customer interest. 
##### Analyze Customer Feedback on Subscription Durations: 
- To understand why most customers do not renew after 12 months, conduct surveys or focus groups aimed at exploring their satisfaction with the service and any improvements they’d like to see. This feedback can guide service enhancements or offer development that addresses the reasons for non-renewal. 




