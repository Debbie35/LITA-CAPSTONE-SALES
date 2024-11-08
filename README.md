# LITA-CAPSTONE DATA ANALYSIS

### PROJECT TITLE: SALES PERFORMANCE ANALYSIS

### PROJECT OVERVIEW
 In this project, I am tasked with analyzing the sales performance of a retail store. I will need to explore sales data to uncover key insights such as top-selling products, regional performance, and monthly sales trends. The goal is to produce an interactive Power BI dashboard that highlights these findings.

### DATA SOURCE
- excel file
- csv file

### TOOLS USED
- Microsoft Excel [Download Here](https://www.microsoft.com)
  1. for Data Cleaning
  2. Analysis and
  3. visualization
- SQL - Structured Query Language
  1. Quering of Data
- Power BI - Power Business Intelligent
  1. Data visualisation
  2.  Report
   
### EXPLORATORY DATA ANALYSIS  DATA ANALYSIS
This is where I include some line of code, queries or some of the DAX expressions used during th analysis;
### WITH EXCEL
In the initial phase of data cleaning and preparations, I perform the following actions;
  - Data loading and inspection
  - Handling missing variables
  - Data Cleaning and Formatting
  - visualization of key findings
## To use pivot:
- Highlight or click on any cell within your data range
- Go to the insert Tab
- Click on the pivotbtable button to open a dialog box
- Select Data Range
- Choose where to place the pivot table (a new worksheet or in the existing worksheet)
- Build customize and format the table

 1. Summarize total sales by Product
   <img width="206" alt="TOTAL SALES OR REVENUE BY PRODUCT" src="https://github.com/user-attachments/assets/e0b16da2-31fe-4ccc-ad01-e54a09fa6d40">
 
2. Summarize total sales by Region
  <img width="221" alt="TOTAL SALES BY REGION" src="https://github.com/user-attachments/assets/909f8f96-994c-44b3-9014-1df8a9270b12">


4. Summarize total sales by Month   
<img width="219" alt="SUM OF TOTAL REVENUE BY MONTH" src="https://github.com/user-attachments/assets/a4c72763-3507-424d-9485-92339d414fe2">



5. Average Sales per product
   <img width="581" alt="CAPSTONE AVERAGE SALES PER PRODUCT" src="https://github.com/user-attachments/assets/cc4835b7-a9dd-4827-bf37-720bbfdf0729">

6. Sum of total revenue by Region  
![SUM OF TOTAL REVENUE BY REGION](https://github.com/user-attachments/assets/3eaa5f71-eb29-4214-b85c-13709dbbd48e)

  
7. Sum of total Revenue by Region using excel function SUMIF
# =SUMIF(range,criteria,[sum_range])
WHERE;
  -  Range : the range of cells to evaluate, in this sense region
  -  Criteria: the conition that must be met (can be any of the 4 regions in this analysis- )
  -  Sum_range:the actual cell to sum
    
```EXCEL
=SUMIF(D2:D50001,D2,H2:H50001)
```
<img width="251" alt="TOTAL REVENUE BY REGION USING EXCEL FUNCTION SUMIF " src="https://github.com/user-attachments/assets/1138da3a-7ac4-4fae-9a31-20a8faf4f1fb">

8.Average sales per product 
# =AVERAGEIF(range,criteria,[average_range])
WHERE;
- Range : the range of cells to evaluate, in this sense product
- Criteria: the condition that must be met (can be any of the 6 products in this analysis)
-  Average_range:the actual cell to average

```EXCEL
=AVERAGEIF(C2:C50001,C49988,H2:H50001)
```
<img width="294" alt="AVERAGE SALES BY PRODUCT USING EXCEL FUNCTION AVERAGE IF" src="https://github.com/user-attachments/assets/c0d8eaa2-f494-4881-8d53-cd560bda9c2c">

9. Percentage Revenue by Region

<img width="320" alt="PERCENTAGE REVENUE BY REGION" src="https://github.com/user-attachments/assets/d52e0097-479b-4a11-88bc-aa482ef70255">

10. Percentage sales by product
    
<img width="281" alt="SALES PER PRODUCT IN PERCENTAGE" src="https://github.com/user-attachments/assets/f5e9b2a9-5d99-4e9c-a3c1-70a187562505">

### EXPLORATORY DATA ANALYSIS (WITH SQL)
 - Convert excel sheet to csv
 - Remove headers
 - import the csv to my sql
 - Ensure to format the the date column into YYY-MM-DD while importing the csv into my sql

 1. Total sales for each product category  

 ```SQL
SELECT Product, SUM(Totalsales) As TotalSales
FROM orders
GROUP BY Product;
```
![sales 1](https://github.com/user-attachments/assets/4acd1fd2-ef59-4e6c-9c91-234a5b3f1095)

2. Number of sales transaction in each region
 ```SQL
SELECT Region, COUNT(*)As NumberOfTransaction
FROM Orders
GROUP BY Region;
```
![sales 2](https://github.com/user-attachments/assets/1ba41b0a-acf6-47ac-a26e-792328fefe2b)

3. Top selling product by total sales value
   ``` SQL
   SELECT Product, SUM(TotalSales) As TotalSales
   FROM orders
   GROUP BY TotalSales DESC
   LIMIT 1;
   ```
   ![sales 3](https://github.com/user-attachments/assets/4d85bee5-0b57-40a6-a918-95083576f3d6)

4.Total revenue per product

```SQL
SELECT Product, SUM(TotalSales)As TotalRevenue
FROM Orders
GROUP BY Product;
```
![sales 4](https://github.com/user-attachments/assets/b56b1767-8b1d-4578-bddf-1d7ec2e85b8c)

5. Monthly sales total for the current year

```sql
SELECT MONTH(OrderDate)As Month, SUM (TotalSales)As MonthlySales
FROM Orders
WHERE YEAR(OrderDate)=YEAR(CURDATED())
GROUP BY MONTH(OrderDate)
ORDER BY MONTH;
```
![sales 5](https://github.com/user-attachments/assets/e321ae74-2adf-4473-9fcc-4deec2203766)

6. Top 5 customer by totalpurchase amount

```SQL
SELECT CustomerID,SUM(TotalSales) As TotalPurchase
FROM orders
GROUP BY CustomerID
ORDER BY TotalPurchase DESC
LIMIT 5;
```
![sales 6](https://github.com/user-attachments/assets/5ed6b234-dc3b-48d4-ae04-944af1ca5945)


7. Percentage of total sales contributed by each region
```SQL
SELECT Region,
SUM(TotalSales) As TotalSales,
(SUN(TotalSaless)/(SELECTSUM(TotalSales)FROM orders)*100) As PercentageOfTotalSales
FROM orders
GROUP BY Region;
```
![sales 7](https://github.com/user-attachments/assets/90e895c4-d3e9-4abc-a341-44955db53eb7)

8. Products with no sale in the last quarter
```SQL
SELECT DISTINCT Product
FROM orders
WHERE Product NOT IN(
SELECT Product
FROM orders
WHERE OrderDate>=DATE_SUB(CURDATE(),INTERVAL 3 MONTH)
);
```
 ![sales 8](https://github.com/user-attachments/assets/b17474e6-2218-4a07-94ea-22677449274f)

 ### DATA VISUALIZATION WITH POWER BI
 # KEY INSIGHTS;
 1. Sales Overview
 2. Top-performing products
 3. Regional breakdown

# SALES OVERVIEW
1. Key Performance Indicator (KPI): A calculated measure in DAX was created for Total sales, Total order and Average order value.
<img width="472" alt="measure 1" src="https://github.com/user-attachments/assets/162907be-1923-4d1c-9afe-fd453774e94d">

Total Sales
  <img width="347" alt="MEASURE 2" src="https://github.com/user-attachments/assets/7cc8457e-e613-42d3-ba33-18088bbc163c">

Total Order
<img width="351" alt="measure 3" src="https://github.com/user-attachments/assets/038c3d6c-3783-4a92-8681-7d4c839eaaa8">

Average Order Value
  Afterwards the three measures were visualized on a card using text box
<img width="492" alt="CARD FROM MEASURES" src="https://github.com/user-attachments/assets/c0d86c1e-6dd1-48b3-b870-19e700fb9b1d">

2. Sales Trend Overtime using a line chart
<img width="476" alt="SALES TREND" src="https://github.com/user-attachments/assets/35cd8873-c452-454b-8e5d-04c52a6458de">

use the TOOLTIPS for additional information (total order and average order)

<img width="476" alt="Tooltips (3)" src="https://github.com/user-attachments/assets/665d9386-10a6-45e3-812d-4148d2fd760e">

use SLICER for Dynamic Time Periods

<img width="152" alt="slicer for dynamic time periods" src="https://github.com/user-attachments/assets/99237b65-c28d-4ea9-af0e-b623a87183c5">

 3. Sales by product type using a pie chart
<img width="411" alt="SALES BY PRODUCT TYPE" src="https://github.com/user-attachments/assets/493c2761-9a9f-4199-aca9-ecb4e565dbfb">

# Top Performing Product Session

 1. Top 3- product by sales using a pie chart
 <img width="419" alt="TOP 3 PERFORMING PRODUCTS" src="https://github.com/user-attachments/assets/661b8822-2613-43ed-b2a6-e912a1d26279">

# REGIONAL BREAKDOWN
 Map Visualization
 
<img width="455" alt="MAP BASE ON REGION" src="https://github.com/user-attachments/assets/7c26d9b9-8cc0-4f15-8568-94f738dbad2d">

A side by side comparison of sales value for each region using pie chart
<img width="440" alt="Sales by region" src="https://github.com/user-attachments/assets/000c5f96-2420-4599-a5db-b47f018c56ae">

