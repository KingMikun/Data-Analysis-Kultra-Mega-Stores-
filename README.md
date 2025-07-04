# Data-Analysis-Kultra-Mega-Stores
## Project Topic: DSA Project-SQL

### Project Overview
This project was undertaken as a case study with the primary objectives of analyzing the provided data thoroughly and presenting the most significant insights and findings derived from the analysis. The analysis aimed to uncover patterns, trends, and actionable recommendations within the dataset to inform strategic decision making.

### Data Source
The source of data used here were two excel file provided by the Business Manager of the Abuja division of KMS containing order data from 2009 to 2012
1. [Download here](https://drive.google.com/file/d/1h1y6xY325lTCX7ImIIegCuzeOCE9JSYp/view?usp=sharing)
2. [Download here](https://drive.google.com/file/d/17NMu_cSbFO6ZQSlgqi38dEG0fJTqAYFW/view?usp=sharing)

### Dataset Description
There are two different sets of data sent. The first contains 8,399 rows with fields containing customers information, their orders and shipping details. The second contains names of customers who returned items.
### Table of Content
- Project Overview
- Data Source
- Dataset Description
- Tools Used
- Exploratory Data Analysis

### Tools Used
 - Microsoft Excel - used for data cleaning, and manipulation.
 - SQL Server Management Studio
    - Data Exploration: querying data, viewing tables and relationships.
    - Data Transformation: to create new columns, group and aggregate.
    - Joining Tables.

### Exploratory Data Analysis
#### CASE SCENARIO 1
Question 1: Which Product category had the highest sales?  
Query
```
SELECT Product_Category, SUM(Sales) AS Total_Sales
from [KMS Sql Case Study]
GROUP BY Product_Category
ORDER BY Total_Sales DESC
```
Answer  
Technology had the highest total sales with ₦5,984,249    

Question 2: What are the Top 3 and Bottom 3 regions in terms of sales?  
Top 3
Query
```
SELECT TOP 3 Region, SUM(SALES) AS Total_Sales
from [KMS Sql Case Study]
GROUP BY Region
ORDER BY Total_Sales DESC
```
Answer:
The top 3 regions in terms of sales are:
- West ₦3,597,549
- Ontario ₦3,063,213
- Prarie ₦2,837,305

Bottom 3
Query
```
SELECT TOP 3 Region, SUM(SALES) AS Total_Sales
from [KMS Sql Case Study]
GROUP BY Region
ORDER BY Total_Sales ASC
```
Answer  
The bottom 3 regions in terms of sales are
- Yukon                    ₦975,867
- Northwest Territories   ₦800,847
- Nunavut                  ₦116,376

Question 3  
What were the total sales of appliances in Ontario?
Query
```
SELECT SUM(SALES) AS Appliance_Sales_Ontario
FROM [KMS Sql Case Study]
WHERE Product_Sub_Category = 'Appliances'
AND Province = 'Ontario'
```
Answer  
The total sales of appliances in Ontario is ₦202,347  

Question 4  
Advise the management of KMS on what to do to increase the revenue from the bottom
10 customers  
Query
```
SELECT TOP 10 Customer_Name, SUM(Sales) AS Total_Sales
FROM [KMS Sql Case Study]
GROUP BY Customer_Name
ORDER BY Total_Sales ASC
```
Answer  
Improve service for low spending customers like:
- Simplify their ordering experience,reach out via call or email, product recommendation.
- Send personalized discount offers, emails promoting limited-time deals for specific product categories.
- Introduce loyalty rewards like: spend ₦20,000 more this month and receive 10% of on your next purchase.  

Question 5  
KMS incurred the most shipping cost using which shipping method?    
Query
```
SELECT Ship_Mode, SUM(Shipping_Cost) AS Total_Shipping_Cost
FROM [KMS Sql Case Study]
GROUP BY Ship_Mode
ORDER BY Total_Shipping_Cost DESC
```
Answer  
The shipping method with the most shipping cost is the 'Delivery Truck' with a total Shipping cost of ₦51,971

#### CASE SCENARIO 2  

Question 6  
Who are the most valuable customers, and what products or services do they typically
purchase?  
Query
```
SELECT TOP 10 Customer_Name, SUM(Sales) AS Total_Sales
FROM [KMS Sql Case Study]
GROUP BY Customer_Name
ORDER BY Total_Sales DESC
SELECT TOP 10 Customer_Name, Product_Name, SUM(Sales) AS Total_Sales
FROM [KMS Sql Case Study]
WHERE Customer_Name IN (
      'Emily Phan',
      'Deborah Brumfield',
      'Roy Skaria',
      'Sylvia Foulston',
      'Grant Carroll',
      'Alejandro Grove',
      'Darren Budd',
      'Julia Barnett',
      'John Lucas',
      'Liz MacKendrick'
      )
GROUP BY Customer_Name, Product_Name
ORDER BY Total_Sales DESC

```

Answer  
These are the most valuable customers
- Emily Phan
- Deborah Brumfield
- Roy Skaria
- Sylvia Foulston
- Grant Carroll
- Alejandro Grove
- Darren Budd
- Julia Barnett
- John Lucas
- Liz MacKendrick

These are the products or services they typically purchase
|Customer_Name|Product_Name|
|------------|------------|
|Emily Phan|Polycom ViewStation™ ISDN Videoconferencing Unit|
|Deborah Brumfield| Hewlett Packard LaserJet 3310 Copier|
|Liz MacKendrick Okidata|  ML591 Wide Format Dot Matrix Printer|
|Deborah Brumfield| Panasonic KX-P3626 Dot Matrix Printer|
|Julia Barnett|Riverside Palais Royal Lawyers Bookcase, Royale Cherry Finish|
|Darren Budd | Sharp AL-1530CS Digital Copier|
|Grant Carroll|   Fellowes PB500 Electric Punch Plastic Comb Binding Machine with Manual Bind|
|Alejandro Grove|         GBC DocuBind TL300 Electric Binding System|
|Sylvia Foulston     |    Polycom ViewStation™ Adapter H323 Videoconferencing Unit|
|Roy Skaria         |Riverside Palais Royal Lawyers Bookcase, Royale Cherry Finish|

Question 7  
Which small business customer had the highest sales?  
Query
```
SELECT TOP 1 Customer_Name, SUM(Sales) AS Total_Sales
FROM [KMS Sql Case Study]
WHERE Customer_Segment = 'Small Business'
GROUP BY Customer_Name
ORDER BY Total_Sales DESC
```
Answer  
The small business customer with the highest sale is 'Dennis Kane' with a sale of ₦75,967  

Question 8  
Which Corporate Customer placed the most number of orders in 2009 – 2012?  
Query
```
SELECT TOP 1 Customer_Name, COUNT(Order_ID) AS Order_Count
FROM [KMS Sql Case Study]
WHERE Customer_Segment = 'Corporate' AND YEAR(Order_Date) BETWEEN 2009 AND 2012
GROUP BY Customer_Name
ORDER BY Order_Count DESC
```
Answer  
'Adam Hart' with an order count of 27    

Question 9  
Which consumer customer was the most profitable one?  
Query
```
SELECT TOP 1 Customer_Name, SUM(Profit) as Total_Profit
FROM [KMS Sql Case Study]
WHERE Customer_Segment = 'Consumer'
GROUP BY Customer_Name
ORDER BY Total_Profit DESC
```
Answer  
Emily Phan with a total profit of ₦34,005  

Question 10  
Which customer returned items, and what segment do they belong to?  
Query
```
SELECT [KMS Sql Case Study].Order_ID,
       [KMS Sql Case Study].Customer_Name,
       [KMS Sql Case Study].Customer_Segment,
       Order_Status.Order_ID,
       Order_Status.Status
FROM [KMS Sql Case Study]
JOIN Order_Status
ON [KMS Sql Case Study].Order_ID = Order_Status.Order_ID
```

Answer  
There were over 500 customers who returned items but due to the large number and for the purpose of this report, these are just 10 of them and the segment they belong to
|Customer_Name|Customer_Segment|  
|-----------|-----------------|  
|Dorothy Badders|Home Office|
|Grant Carroll|Corporate|
|Edward Hooks|Consumer|
|Carlos Soltero|Small Business|
|Brendan Dodson|Corporate|
|Rick Reed |Consumer|
|Julia West |Home Office|
|Brad Eason| Small Business|
|Charlotte Melton |Home Office|
|Hunter Glantz |Corporate|  

Question 11  
If the delivery truck is the most economical but the slowest shipping method and
Express Air is the fastest but the most expensive one, do you think the company
appropriately spent shipping costs based on the Order Priority? Explain your answer  
Query
```
SELECT Order_Priority, Ship_Mode, COUNT(Order_ID) AS Order_Count,
SUM(Sales - Profit) AS Estimated_Shipping_Cost,
AVG(DATEDIFF(day, Order_Date, Ship_Date)) AS Average_Ship_Days
FROM [KMS Sql Case Study]
GROUP BY Order_Priority, Ship_Mode
ORDER BY Order_Priority, Ship_Mode DESC
```
Answer  
No, the company did not appropriately spend on shipping based on order priority.  
Due to these reasons:  
- Critical orders should use Express Air more than Delivery Truck.
- Low priority orders should not use Express Air, especially when it still takes 4 days to ship.
- Delivery Truck is costly here, even though it’s meant to be cheap.
- Too many 1-day deliveries even for low and medium priorities. It is overuse of premium shipping.
