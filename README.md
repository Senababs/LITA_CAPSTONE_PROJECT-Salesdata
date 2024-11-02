![20241027_182630](https://github.com/user-attachments/assets/3fe9e5a3-0837-4ee1-9928-a0b930ae49e6)
![20241027_182951](https://github.com/user-attachments/assets/51db4c12-c4ca-4e1c-a802-b804eb0a0c9e)
## LITA_CAPSTONE_PROJECT 1

## Project Title: Sales Data
## Project Content
- [Project Title](#project-title)
- [Project Content](#project_content)
- [Project Overview](#project_overview)
- [Project Aim & Objectives](#project_aim_and_objective)
- [Data Source and Methodology](#data_sources_and_methodology)
- [Analytical Result](#analytical_result)
- [Conclusion](#conclusion)

## Project Overview
This project focuses on analyzing the sales performance of six clothing items across four regions in a retail store during the years 2023 and 2024.

## Project Aim & Objectives
 The primary aim of this project is to identify opportunities for growth and optimization within the retail store's clothing sales by examining product popularity, regional trends, customer behavior, and pricing strategies.

Project Objectives
- Determine the best-selling products and their impact on revenue.
- Identify regions with the highest sales volume.
- Analyze customer purchasing patterns.
- Understand seasonal trends within each month of 2023 and 2024

## Data Source and Methodology
Dataset was provided by Incubator hub instructors. 
-  The variables includes:
     - Order ID: distinct code assign to each sales transaction
     - Customer ID: distinct code given to each customers used for multiple transactions
     - Product: Items sold (Gloves, Jacket, Hat, Shoes, Socks and Shirt)
     - Region: Location of sales transaction (East, West, South and North)
     - Order Date: Date of sales transaction
     - Unit Price: Price assigned to one of each items sold
     - Quantity: number of units of the product sold in the transaction.
     
   - Data Info
      - Data Format: Excel.
      - Data Quality: Omitted Revenue column (total income generated sales of product).
        
   - Analytical tools: Download link on other repository
       - Microsoft Excel (Ms Excel)
         - Data cleaning
          -Revenue column was added and calculated using this function
 
                =Revenue (Unit Price * Quantity)
       - Pivot table was used to summarise total sals by product, region and month.
        - Metrics such as Average sales per product and total revenue by region where calculated
          - Example for Average sales of shirt:
 
                     =AVERAGEIFS(H2:H9922, C2:C9922,M6)
 
          - And Total revenue for East region

                 =SUMIFS(H2:H9922, D2:D9922,M16)

      - Structured Query Language (SQL)
          - The dataset was converted to Comma seperated values to load into the SQL server
          - The following queries were written to analyse the sales performance
              - 1. Retrieve the total sales for each product category.

                        select Product, sum(Revenue) as Total_sales from [dbo].[LITA CAPSTONE_PROJECT_SALESDATA] Group by Product
                2. Find the number of sales transcations in each region.

                        select Region, count(Orderid) as Number_of_sales_transaction from [dbo].[LITA CAPSTONE_PROJECT_SALESDATA] group by Region
                3. Find the highest selling product by total sales value.
               
                          select top 1 Product, sum(quantity) as Total_sales  from [dbo].[LITA CAPSTONE_PROJECT_SALESDATA] Group by Product order by sum(quantity) desc
                4. Calculate total revenue per product
            
                       select Product, sum(Revenue) as Total_revenue from [dbo].[LITA CAPSTONE_PROJECT_SALESDATA] group by product
                5. Find the top 5 customers by total purchase amount

                        select top 5 Customer_id, sum(revenue) as Total_Purchase_Amount from [dbo].[LITA CAPSTONE_PROJECT_SALESDATA] Group by customer_id order by sum(revenue) desc
                6. Calculate monthly sales totals for the current year

                        Select FORMAT(OrderDate, 'MM-2024') as Month, sum(Revenue) as Monthly_sales from [dbo].[LITA CAPSTONE_PROJECT_SALESDATA] where year(OrderDate) =2024 group by FORMAT(OrderDate, 'MM-2024') ORDER BY Month
                7. Calculate the percentage of total sales contributed by each region

                        select region, sum(Quantity) as total_sales, (sum(quantity) * 100.0 / (select sum(quantity) from [dbo].[LITA CAPSTONE_PROJECT_SALESDATA])) as Percentage_regional_sales from  [dbo].[LITA CAPSTONE_PROJECT_SALESDATA] Group by Region 

                8. Identify products with no sales in the last quarter
 
                               select distinct product from  [dbo].[LITA CAPSTONE_PROJECT_SALESDATA] Where  Product not in (select Product  from [dbo].[LITA CAPSTONE_PROJECT_SALESDATA] where OrderDate >= '2024-10-01' and OrderDate < '2025-01-01');
      - Power Business intelligence (Power Bi).
           - For creation of dashboard that visualizes the insights found in excel and SQL
           - The dashboard include sales overview, top performing products, regional and yearly breakdown
## Analytical Result
   - Data Visualization
     

![20241027_182630](https://github.com/user-attachments/assets/fd3d9a17-cd72-4c74-930b-d89a6a2d00da)

![20241027_182951](https://github.com/user-attachments/assets/974b4843-51cf-4846-ae6c-e4765d8eb27e)


- Data observation

     - *Product Performance*: It was observed that the "Shoes" product immediately before the 'Hat' product (The highest selling product by units sold), stands out as the top-selling product by revenue. This can be attributed to its widespread appeal across three out of the four regions, while other products are limited to one or two regions. With the 'Jacket' product being the second and least performing products.
      
     - *Region Performance*: The South region emerges as the highest-performing region in terms of revenue. However, it's noteworthy that only three products are consumed by customers in this region. Whereas customers in the West region consume 4 of the products still it is the least performing region by revenue.
        
     - *Yearly trend*: A higher overall revenue has been observed in 2023 compared to 2024, although 2024 Orderdate stops in the month of May. Also it was quite noticeable that these products were highly consumed in certain of each year. For example: The product 'Gloves' sold more in the month of June & December 2023 also in June 2024.
     
   - Key Suggestion
       - Understanding the specific demands and preferences of each region can help tailor product offerings and marketing efforts.
       - Leverage seasonal trends and holidays to create targeted promotions.
       - Adjust unit pricing strategies accordingly.

  ## Conclusion ##
This dataset shows the every region has it one products preferences and customer's purchasing capability. It also shows how preferences in product sold changes across different time of the year, all of which contribute to the revenue generated by the retail store.  Taking into account some of the suggestions earlier stated can optimize the sales at the store.

     
      
