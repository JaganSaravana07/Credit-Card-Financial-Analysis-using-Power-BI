# Credit Card Financial Analysis
## Introduction
The Credit Card Financial Dashboard provides a comprehensive analysis of customer transactions, revenue patterns, and spending behavior. This interactive dashboard empowers businesses to make data-driven decisions, optimize customer engagement, and enhance financial performance.
Through data visualization, key insights into customer spending habits, transaction trends, and business revenue streams are presented in an easily interpretable format.

## Objectives
### 1. Understanding Revenue & Transactions
- Track revenue trends on a quarterly and yearly basis.
- Analyze revenue distribution by transaction type (bills, groceries, entertainment, etc).
- Identify revenue contribution based on customer segments like age group, income level, job type, and education level.
- Assess transaction volume and revenue contribution by different card categories (Blue, Silver, Gold, Platinum).
- Assess revenue trends across different states and regions to identify high-performing locations.
### 2. Customer Insights & Segmentation
- Evaluate customer behavior based on education, job type, and income group.
- Identify high-value customers and analyze revenue contribution by demographic segments.
- Determine how customer satisfaction and spending patterns impact revenue growth.
### 3. Transaction Behavior Analysis
- Compare revenue based on different payment methods (Swipe, Chip, Online).
- Track weekly and monthly transaction trends for demand forecasting.
- Assess customer acquisition cost and retention strategies for different credit card categories.

## Import data to SQL database
1. Prepare CSV file
2. Create tables in SQL
3. Import CSV file into SQL
*Note: I used Postgresql Database*

## DAX Queries Used
1. `AgeGroup = SWITCH(
     TRUE(),
     'public cust_detail'[customer_age] < 30, "20-30",
     'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
     'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
     'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
     'public cust_detail'[customer_age] >= 60, "60+",
     "unknown"
   )`
2. `IncomeGroup = SWITCH(
     TRUE(),
     'public cust_detail'[income] < 35000, "Low",
     'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] <70000, "Med",
     'public cust_detail'[income] >= 70000, "High",
     "unknown"
   )`
3. `week_num2 = WEEKNUM('public cc_detail'[week_start_date])`
4. `Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]`
5. `Current_week_Reveneue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
    ALL('public cc_detail'),
    'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])))`
6. `Previous_week_Reveneue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
    ALL('public cc_detail'),
    'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1))`

## Conclusion & Key Takeaways
- Steady Quarterly Growth: Revenue and transaction count show consistent growth across Q1–Q4, with Q4 being the highest-performing quarter ($14.5M revenue).
- Dominant Revenue Categories: Bill payments, groceries, and entertainment drive the highest revenue, while travel and food expenditures contribute significantly.
- Customer Spending Trends:
  - Higher-income groups and business owners contribute the most revenue.
  - Graduates and white-collar professionals are key spending demographics.
- Card Type Performance: Blue card dominates transactions, while Gold & Platinum cards show potential for premium customer engagement.
- Payment Methods: Swipe transactions account for the majority of payments ($36M), while online transactions remain underutilized ($4M).
- Geographic Revenue Trends: California, New Jersey, Texas, and New York lead in credit card

## Recommendations
1. Enhancing Customer Engagement & Retention
  a. Expand loyalty programs & cashback offers to encourage repeat transactions, especially in high- spending categories (bills, groceries, travel).
  b. Improve customer satisfaction (currently 3.19/5) by reducing transaction fees, offering better rewards, and personalizing services.
  c. Develop premium card incentives to attract high- net-worth customers, increasing Gold & Platinum card adoption.
2. Optimizing Revenue Growth & Transaction Behavior
  a. Encourage online transactions by offering higher rewards, enhanced security features, and exclusive digital promotions.
  b. Leverage customer segmentation insights to offer tailored benefits based on age, income, and education level.
  c. Capitalize on high-revenue states (CA, NJ, TX, NY) by launching region-specific marketing campaigns and financial services.
3. Expanding Market Reach & Acquisition
  a. Reduce customer acquisition costs for lower- performing segments by implementing AI-driven targeting and digital onboarding strategies.
  b. Increase financial inclusivity by introducing low- interest products for middle-income and younger customers.
  c. Expand advertising and partnership efforts in growing markets (Florida, Texas, emerging urban centers).

