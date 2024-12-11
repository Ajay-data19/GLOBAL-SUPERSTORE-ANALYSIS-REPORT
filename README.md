# Superstore Analysis Report
![Screenshot 2024-12-11 164718](https://github.com/user-attachments/assets/8c694ff9-0003-415f-a280-fd3c0d5a1059)


## Project Overview
In today's business landscape, data-driven decision-making is essential for success. The Superstore Analysis Project leverages the power of data to uncover patterns, trends, and key insights within a sales dataset. By employing advanced analytics and visualization techniques, this project assists stakeholders in understanding historical sales performance, profit distribution and customer behaviour patterns.

## Problem Statement
The superstore faces challenges in effectively leveraging its vast amounts of sales data to identify key patterns, trends, and actionable insights. Despite having extensive data, stakeholders struggle to use this information to enhance decision-making in critical areas such as sales performance, profitability, and customer behavior. This project aims to address these challenges by conducting a comprehensive analysis focused on sales trends, profit margins, and customer behavior, employing advanced analytics and visualization techniques. The goal is to provide a clear understanding of historical performance and predictive insights to drive strategic decisions that improve operational efficiency, optimize inventory management, enhance customer satisfaction, and increase overall profitability.

## Process
`Data Preparation`
- The initial phase involved performing data cleaning tasks, such as removing null values, eliminating unnecessary columns, handling duplicates, and adjusting data types to ensure the data was well-prepared for analysis.
  
- `Data Modeling`
- The Next step was to create calculated measures and columns using DAX (Data Analysis Expressions) in Power BI, enhancing the dataset's analytical capabilities.

<pre><code>
# Calculated Total Cost
  Total Cost = SUM(Superstore[Sales]) - SUM(Superstore[Profit])

# Calculated Profit Margin
  Profit Margin (%) = DIVIDE(SUM(Superstore[Profit]),SUM( Superstore[Sales])) * 100

# Calculated Total Unique Customer
  TotalCustomers = DISTINCTCOUNT('Superstore'[Customer ID])
 
# Number of Transactions
  NumberOfTransactions = COUNTROWS('Superstore')

# Created Columns for Firstpurchae and Lastpurchase
  FirstPurchaseDate = CALCULATE(MIN('Superstore'[Order Date]), ALLEXCEPT('Superstore', 'Superstore'[Customer ID]))

  LastPurchaseDate = CALCULATE(MAX('Superstore'[Order Date]), ALLEXCEPT('Superstore', 'Superstore'[Customer ID]))

# Created CustomerLifespan column
  CustomerLifespan = DATEDIFF('Superstore'[FirstPurchaseDate], 'Superstore'[LastPurchaseDate], MONTH)

# Average Customer Lifespan
  AvgCustomerLifespan = AVERAGE('Superstore'[CustomerLifespan])

# Average Purchase Value
  AveragePurchaseValue = [TotalSales] / [NumberOfTransactions]

# AveragePurchaseFrequencyRate = [NumberOfTransactions] / [UniqueCustomers]

# Customer Life Value
  CLV = [AveragePurchaseValue] * [AveragePurchaseFrequencyRate] * [AvgCustomerLifespan]

# Created Purchase Count Column 
  PurchaseCount = COUNTROWS(FILTER('Superstore', 'Superstore'[Customer ID] = EARLIER('Superstore'[Customer ID])))

# Customers With More Than One Purchase
  CustomersWithMoreThanOnePurchase = CALCULATE(DISTINCTCOUNT('Superstore'[Customer ID]), FILTER('Superstore', [PurchaseCount] > 1))
  
# Calculated Repeat Purchase Rate of Customers
  RepeatPurchaseRate = ([CustomersWithMoreThanOnePurchase] / [TotalCustomers]) * 100
  
</code></pre>

`Data Analysis`
- Following data modeling, an in-depth data analysis was conducted within Power BI, utilizing various visualization techniques like matrices to identify trends in sales, category-wise performance, sub-category wise performance, geographic Distribution, profit details and customer behaviour. This analysis provided actionable insights into market dynamics and supported strategic decision-making.

`Dashboard Developement`
- The project focused on creating a dynamic and user-centric dashboard in Power BI. This dashboard leveraged advanced visualization techniques and incorporated bookmmarks, slicers and drill-through features to enable intuitive data exploration and detailed analysis. These functionalities allowed users to interact with the data effortlessly and gain tailored insights, enhancing decision-making capabilities.

## Dashboard Overview  

This project focuses on creating an interactive and insightful dashboard using Power BI. The dashboard is divided into two pages, each serving a specific purpose with tailored KPIs and functionalities.  

### Page 1: Sales and Profit Analysis  
- An in-depth exploration of sales and profit metrics with bookmark functionality to toggle between Sales and Profit views.  
- **Key Performance Indicators (KPIs):**  
  - Total Sales  
  - Total Cost  
  - Total Profit  
  - Profit Margin  
- **Interactive Features:**  
  - Filters and slicers to analyze data based on category and time period.  

### Page 2: Customer Behavior Analysis  
- A detailed evaluation of customer behavior patterns to understand purchasing trends.  
- **Key Performance Indicators (KPIs):**  
  - Total Customers  
  - Average Purchase Value  
  - Customer Lifetime Value  
  - Repeat Purchase Rate  
- **Interactive Features:**  
  - Filters and slicers to dynamically explore data across categories and timeframes.  

This dashboard aims to deliver actionable insights through a user-friendly and dynamic interface.  
![Screenshot 2024-12-11 164809](https://github.com/user-attachments/assets/210a87a5-8ae5-43d8-add8-396334f2eb50)
![Screenshot 2024-12-11 164900](https://github.com/user-attachments/assets/2de6b9bb-b8f1-4e99-80d6-85af64ba2ba4)
![Screenshot 2024-12-11 164941](https://github.com/user-attachments/assets/b86bfc29-f9b1-471e-a4f9-ca3c44b345e5)

**[Click here to access the interactive dashboard](https://app.powerbi.com/view?r=eyJrIjoiNWYwMmI4OWQtYmY2MS00NGJhLTk4ZTItMDkzZjJjNDE5YzhjIiwidCI6ImY0M2MzMTgyLTcxZjAtNGRjOS04YjA0LTc0OTMwZTNmOGNkYSJ9)** 

## Key Insights

1. **Category Performance**  
   - Technology category outperforms Furniture and Office Supplies in both sales and profit.  
2. **Segment Dominance**  
   - Consumer segment leads in both customer count and revenue, outperforming Corporate and Home Office segments.  
3. **Regional Analysis**  
   - **Top-performing regions by sales**: Central, South, North, Oceania, and Southeast Asia.  
   - **Top-performing regions by profit**: Central, Central Asia, North, North Asia, and South.  
   - **Underperforming regions**: Africa, EMEA, and Canada need strategic improvement.  
4. **Country Trends**  
   - **Top countries by sales**: USA, Australia, China, France, and Germany.  
   - **Top countries by profit**: USA, China, India, Australia, and France.  
   - Some countries report negative profit rates, highlighting areas for improvement.  
5. **Sales and Profit Trends**  
   - Year-over-year growth observed, with significant sales and profit spikes during specific periods.  
6. **Customer Behavior**  
   - Repeat Purchase Rate: 99.56%, indicating high customer retention.  
   - Discounts positively correlate with sales, increasing purchase frequency.  
   - Consumer segment has the highest customer count.  
7. **Order Priority**  
   - High and medium-priority orders account for 60% of total orders.  
8. **Purchase Value**  
   - Technology category has a high average purchase value (50%).  
   - Office Supplies category has a low average purchase value (12%).  

---

## Recommendations
1. **Focus on Technology Category**  
   - Expand offerings to maintain dominance.  
2. **Boost Office Supplies**  
   - Introduce bundle deals or premium product options to increase average purchase value.  
3. **Target Underperforming Segments**  
   - Create campaigns and incentives for Corporate and Home Office segments.  
4. **Regional Strategy Improvements**  
   - Focus efforts on high-potential regions like APAC, EU, and the US.  
   - Address performance gaps in Africa, EMEA, and Canada.  
5. **Address Negative Profit Rates**  
   - Investigate inefficiencies or pricing issues in countries with negative profit rates.  
6. **Capitalize on Trends**  
   - Leverage sales spikes for seasonal marketing campaigns.  
   - Increase discounts during specific months to boost sales further.  
7. **Enhance Loyalty Programs**  
   - Strengthen personalized experiences to maintain a high repeat purchase rate.  
8. **Optimize Order Priority**  
   - Streamline supply chain to increase high-priority order fulfillment.  
9. **Innovate Products and Packaging**  
   - Develop attractive product options for low-performing categories.  
   - Continue innovating popular packaging formats.  

