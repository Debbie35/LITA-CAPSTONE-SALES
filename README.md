# LITA-CLASS-PROJECT

### PROJECT TITLE: LITA CAPSTONE DATA ANALYSIS:SALES PERFORMANCE ANALYSIS

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
   
### EXPLORATORY DATA ANALYSIS (WITH EXCEL)
In the initial phase of data cleaning and preparations, I perform the following actions;
  - Data loading and inspection
  - Handling missing variables
  - Data Cleaning and Formatting
  - visualization of key findings
1. Use pivot table to summarize total sales by product
    Column1	AVERAGE SALES PER PRODUCT
SHIRT         =	326.67
SHOE          =	308.75
HAT             =	158.75
SOCKS        =	121.67
JACKET       =	140.00
GLOVES      =	200.00
TOTAL        =	1,255.83
### EXPLORATORY DATA ANALYSIS (WITH SQL)
 - Convert excel sheet to csv
 - Remove headers
 - import the csv to my sql
 - Ensure to format the the date column into YYY-MM-DD while importing the csv into my sql
1. Top selling product by total sales value
   ``` SQL
   SELECT Product, SUM(TotalSales) As TotalSales
   FROM orders
   GROUP BY TotalSales DESC
   LIMIT 1;
   ```
 2. Total sales for each product category  

 ```SQL
SELECT Product, SUM(Totalsales) As TotalSales
FROM orders
GROUP BY Product;

```
3. Number of sales transaction in each region
 ```SQL
SELECT Region, COUNT(*)As NumberOfTransaction
FROM Orders
GROUP BY Region;
```
4.Total revenue per product

```SQL
SELECT Product, SUM(TotalSales)As TotalRevenue
FROM Orders
GROUP BY Product;
```
5.Monthly sales total for the current year

```sql
SELECT MONTH(OrderDate)As Month, SUM (TotalSales)As MonthlySales
FROM Orders
WHERE YEAR(OrderDate)=YEAR(CURDATED())
GROUP BY MONTH(OrderDate)
ORDER BY MONTH;
```

6. Top 5 customer by totalpurchase amount

```SQL
SELECT CustomerID,SUM(TotalSales) As TotalPurchase
FROM orders
GROUP BY CustomerID
ORDER BY TotalPurchase DESC
LIMIT 5;
```

7. Percentage of total sales contributed by each region
```SQL
SELECT Region,
SUM(TotalSales) As TotalSales,
(SUN(TotalSaless)/(SELECTSUM(TotalSales)FROM orders)*100) As PercentageOfTotalSales
FROM orders
GROUP BY Region;
```
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
EDA involves the exploring of Data to answer some questions about the Data such as;
- top-selling product
- monthly sales trend
- sales for each product category
- number of sales transaction in each region
- highest selling product by total sales value
- total revenue per product
- monthly sales total for the current year
- the top 5 customers by total purchase amount
- percentage of total sales contributed by Each region
- identify product with no sales in the last quarter

### DATA ANALYSIS
This is where I include some line of code, queries or some of the DAX expressions used during th analysis;

     

   
   
