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

- **Category Dominance**:  
  I observed that the "Technology" category significantly outperforms both "Furniture" and "Office Supplies" in terms of both sales and profit. Prioritizing this category can amplify growth.  
- **Segment Trends**:  
  The **Consumer segment** leads across all metrics, overshadowing the Corporate and Home Office segments. This indicates a strong preference and engagement from individual buyers.  
- **Regional Performance**:  
  - Top-performing regions by **sales**: Central, South, North, Oceania, and Southeast Asia.  
  - Top-performing regions by **profit**: Central, Central Asia, North, North Asia, and South.  
  - Regions such as **Africa, EMEA, and Canada** underperform, requiring immediate attention.  
- **Country Highlights**:  
  - **Top sales contributors**: USA, Australia, China, France, and Germany.  
  - **Top profit generators**: USA, China, India, Australia, and France.  
  - I noticed some countries showing negative profit rates, which is a concerning trend that needs investigation.  
- **Sales Trends**:  
  Year-over-year analysis reveals consistent sales and profit growth, with distinct spikes during specific months.  
- **Customer Behavior**:  
  - Repeat Purchase Rate: An impressive 99.56%, demonstrating exceptional customer loyalty.  
  - Discounts show a strong positive correlation with increased purchase frequency, particularly during promotional periods.  
- **Order Prioritization**:  
  High and medium-priority orders make up 60% of all orders, highlighting opportunities to optimize logistics for these categories.  
- **Purchase Value Analysis**:  
  - Technology boasts a high **average purchase value** (50%), while Office Supplies lag behind at 12%.  

## Recommendations
1. **Prioritize Technology**:  
   - I recommend channeling more resources into the Technology category to maintain its dominance and capitalize on its high profit margins.  
2. **Boost Underperforming Segments**:  
   - Develop targeted marketing strategies and promotions for the Corporate and Home Office segments to bridge the performance gap.  
3. **Regional Expansion**:  
   - Focus on bolstering sales strategies in high-potential regions such as APAC, EU, and the US. Simultaneously, address inefficiencies in underperforming regions like Africa, EMEA, and Canada through localized campaigns.  
4. **Address Negative Profit Rates**:  
   - Investigate the causes behind negative profit rates in certain countries and implement corrective measures such as pricing adjustments or operational optimizations.  
5. **Leverage Sales Spikes**:  
   - I noticed distinct sales spikes in specific months. Launch well-timed marketing campaigns and seasonal discounts to maximize revenue during these periods.  
6. **Optimize Discounts and Promotions**:  
   - Since discounts strongly correlate with increased sales, continue using this strategy, especially during low-demand periods.  
7. **Strengthen Customer Loyalty**:  
   - Enhance loyalty programs and personalized offers to maintain the high repeat purchase rate and attract new customers.  
8. **Enhance Order Fulfillment**:  
   - Streamline the supply chain for high and medium-priority orders to meet customer expectations more efficiently.  
9. **Increase Purchase Value**:  
   - Introduce bundled deals or premium options in the Office Supplies category to raise its average purchase value.  
10. **Foster Continuous Innovation**:  
     - Regularly introduce new product variations and packaging innovations, especially in high-performing categories, to keep customers engaged.  

## Limitation and Challenges
`Absence of Demographic Data`

The dataset lacked demographic columns such as gender, age group, or income level, making it challenging to perform customer segmentation or identify key target groups. This gap limits the depth of insights that can be derived about customer behavior and preferences.

`Effective Presentation` 

Presenting the findings in the most suitable and effective manner required careful consideration.

`Strategic Recommendations`

Despite a strong understanding of the business, crafting actionable suggestions for business growth demanded thoughtful analysis.

## Learnings
`Data Organization`

Despite the limited dataset, the data's organization and informativeness became evident during this analysis.

`Data Visualization`

Overcoming the challenge of presenting outcomes was achieved through applying knowledge of data visualization techniques and learning new methods.

`Strategic Insights`

Leveraging my profound business understanding and investing time in strategic thinking led to valuable insights, connecting important dots within the data.

## Additional Information
- **Cleaned Dataset**: The full cleaned dataset is uploaded in the main section for reference and further analysis.
- **Interactive Dashboard**: You can access the interactive dashboard through the link provided in the 'Dashboard' section of this README file.

## Tech Stack
Project relies on the following key technologies:

- `Power BI Desktop` Design, visualization, and interactive reporting.
- `DAX (Data Analysis Expressions)` Creation of calculations and measures supporting data visualizations.
- `Power Query` Clean and transform raw data into a structured format.

## License
This project is licensed under the MIT License, allowing you to use, modify, and distribute the code and visuals while maintaining the original license terms.

---

For questions or feedback, please contact: ajaysonkatar@gmail.com

Enjoy exploring the project!
