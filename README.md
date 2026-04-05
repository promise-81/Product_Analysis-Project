# Product_Analysis-Project

## Table of contents 

-	[Project Overview](#Project-Overview)
-	[Data Source](#Data-Source)
-	[Tool Used](#Tool-Used)
-	[Data Understanding](#Deliverables)
-	[Exploratory Data Analysis](#Exploratory-Data-Analysis)
-	[Results/Findings](#Results/Findings)
-	[Recommendations](#Recommendations)
-	[Limitations](#Limitations)
-	[References](#References)

  ### Project Overview 

This high-level Analytical project provides insights on key product metrics to track performance trends effectively and support decision making 

  ### Data Source 

- 3 Csv files
```
  - Product_Data : Contains the product information (Product_Id, product_name, Category, Cost price, Sale Price, Brand, Description,Image_url)
  - Discount_Data : Contains the Discount info (Type of Discount, Discount_Band, month, Discount_applied)
  - Product_Sales : Contains the (Sales_Date, customer_type, Country, Product_name, Discount_bland, number_of_units_sold)
 ```

*Data File Available for Download*
  
   ### Tool used
  
- SQL - For Data Exploration, Data Understanding,
- Power BI - For Data Visualization

  *SQL and Power BI Integrated*


 ### Deliverables
  
- A High Level One page Report overview
- Top Performing regions
- Comparable  revenue trends over time
- Summary of Proft and Units sold Year-over-year(YoY) Change
- Revenue Distribution across Categories
- Revenue and Profit Breakdown Table


 ### Exploratory Data analysis 

After Data and Business Understanding I used CTE Expressions for optimization, to callout the required Columns. Calculated the Revenue, Profit, Total Cost, etc. Proceeded to join product_data and Product_sales table, joimed Product_sales with Discount_Data.

SQL
 ```sql
WITH CTE AS(
SELECT
A.Product,
A.Category,
A. Brand,
A. Description,
A. Sale_price,
A. Cost_price,
A.Image_Url,
B.Date,
B.Customer_Type,
B.Discount_Band,
B.Units_sold,
(sale_price * units_sold) as Revenue,
(cost_price * units_sold) as Total_Cost,
FORMAT ([date],'MMMM') AS Month,
FORMAT ([DATE],'yyyy') AS Year
FROM [dbo].[Product_data] A
JOIN [dbo].[product_sales] B
ON A.Product_ID = B.Product)

SELECT *,
(1- CAST(Discount AS decimal(10,2))* 1.0/100) * Revenue AS DISCOUNT_REVENUE 
FROM CTE A
JOIN [dbo].[discount_data]B
ON A.Discount_Band = B.Discount_Band And A.Month = B.month
```

### Results/findings
Analysis Results Summary 

- Canada emerged the top performing region with an overall revenue of **$613,913.**
- Revenue indicated an unsteady trend spiking high to **$214,612 in June 2022**, from a lowest drop **$72,119 in May 2022**.
- A **6.7%** and **8.%** increase in Total profit and Total Units-sold from previous year respectively
- The Government is the is the highest revenue source with approximately **$1.3 million** in revenue and **$273k** in profit
- High Discount drove **39.93%** of Total revenue, Medium discount **34.5%**, low Discount **23.9%**,  and None Discount band **6.6%**


### Recommendations
- Conduct a root cause analysis for unsteady revenue trends
- Employ personalized Discount Bands on Customer Type to drive revenue growth and profit 

 ### Limitations 
 
**NONE**

 ### References 
 [Product Analysis Reference](https://youtu.be/6MOyrQLCi3w?si=zgTYCVaj-7I_o5Lo)
