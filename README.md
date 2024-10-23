# Walmart_Sales_Analysis


## Overview

This project aims to analyze Walmart's sales data to identify top-performing branches and products, explore sales trends, and understand customer behavior. The goal is to provide insights that can help improve and optimize sales strategies. The dataset used in this analysis is from the [Kaggle Walmart Sales Forecasting Competition](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting).

In this competition, participants are given historical sales data from 45 Walmart stores across different regions. Each store contains various departments, and the challenge is to predict sales for each department. Holiday markdown events, which are known to affect sales, add complexity to the predictions as participants must determine which departments are impacted and to what extent.

## Project Objectives

The primary goal of this project is to analyze Walmart’s sales data to identify the factors that influence sales across different branches.

## Data Description

The dataset was sourced from the [Kaggle Walmart Sales Forecasting Competition](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting). It contains sales transactions from three Walmart branches located in Mandalay, Yangon, and Naypyitaw. The dataset consists of 17 columns and 1000 rows, as detailed below:

| Column                  | Description                                | Data Type      |
|-------------------------|--------------------------------------------|----------------|
| invoice_id              | Sales invoice ID                           | VARCHAR(30)    |
| branch                  | Branch where the sale occurred             | VARCHAR(5)     |
| city                    | City of the branch                         | VARCHAR(30)    |
| customer_type           | Type of customer                           | VARCHAR(30)    |
| gender                  | Customer's gender                          | VARCHAR(10)    |
| product_line            | Product category                           | VARCHAR(100)   |
| unit_price              | Price of each product                      | DECIMAL(10, 2) |
| quantity                | Number of products sold                    | INT            |
| VAT                     | Tax on the purchase                        | FLOAT(6, 4)    |
| total                   | Total cost of the purchase                 | DECIMAL(10, 2) |
| date                    | Date of the purchase                       | DATE           |
| time                    | Time of the purchase                       | TIMESTAMP      |
| payment_method          | Payment method used                        | DECIMAL(10, 2) |
| cogs                    | Cost of Goods Sold                         | DECIMAL(10, 2) |
| gross_margin_percentage | Gross margin as a percentage               | FLOAT(11, 9)   |
| gross_income            | Gross income from the sale                 | DECIMAL(10, 2) |
| rating                  | Customer rating for the product            | FLOAT(2, 1)    |

## Analysis Overview

### 1. Product Analysis

- Analyze the data to understand product line performance, identifying which lines are most successful and which may need improvement.

### 2. Sales Analysis

- Explore sales trends for different products. This analysis will assess the effectiveness of current sales strategies and suggest improvements.

### 3. Customer Analysis

- Segment customers, examine purchase trends, and determine the profitability of different customer types.

## Methodology

### 1. Data Wrangling

This step involves inspecting the data to identify and address any missing or NULL values.

- **Step 1:** Create a database and load the data.
- **Step 2:** Select columns with NULL values. In this dataset, NULL values have been pre-filtered since all fields were set as **NOT NULL** when creating the database.

### 2. Feature Engineering

New columns will be created to derive additional insights from the existing data:

- **Time of Day:** A column that categorizes sales into Morning, Afternoon, and Evening to identify peak sales periods.
- **Day of Week:** A column that extracts the day of the week from the transaction date (Mon, Tue, Wed, etc.) to understand which days are the busiest.
- **Month of Year:** A column that extracts the month from the transaction date (Jan, Feb, Mar, etc.) to analyze sales trends over the year.

### 3. Exploratory Data Analysis (EDA)

Exploratory data analysis will be performed to answer key business questions and meet project objectives.

### 4. Conclusion

The analysis will conclude with actionable insights and recommendations based on the data.

## Business Questions

### General

1. How many unique cities are represented in the data?
2. In which city is each branch located?

### Product Analysis

1. How many unique product lines are there?
2. What is the most common payment method?
3. Which product line has the highest sales volume?
4. What is the total revenue by month?
5. Which month had the highest Cost of Goods Sold (COGS)?
6. Which product line generated the highest revenue?
7. Which city had the largest revenue?
8. Which product line had the highest VAT?
9. Which product lines performed above or below average in sales?
10. Which branch sold more products than the average?
11. What is the most common product line purchased by gender?
12. What is the average rating for each product line?

### Sales Analysis

1. How many sales were made at different times of the day per weekday?
2. Which customer type generates the most revenue?
3. Which city has the highest VAT percentage?
4. Which customer type pays the most VAT?

### Customer Analysis

1. How many unique customer types exist in the data?
2. How many unique payment methods are there?
3. What is the most common customer type?
4. Which customer type makes the most purchases?
5. What is the gender distribution of customers?
6. How is gender distributed across branches?
7. During which time of day do customers leave the most ratings?
8. What is the rating distribution by time of day per branch?
9. Which day of the week receives the highest average ratings?
10. Which branch receives the highest average ratings on specific days?

## Revenue and Profit Calculations

- **COGS (Cost of Goods Sold):** \( \text{COGS} = \text{unit price} \times \text{quantity} \)
- **VAT (Value Added Tax):** \( \text{VAT} = 5\% \times \text{COGS} \)
- **Total Sales:** \( \text{Total} = \text{COGS} + \text{VAT} \)
- **Gross Profit:** \( \text{Gross Profit} = \text{Total} - \text{COGS} \)
- **Gross Margin Percentage:** \( \text{Gross Margin} = \frac{\text{Gross Profit}}{\text{Total Sales}} \)

### Example Calculation

- **Unit Price:** $45.79
- **Quantity:** 7

1. **COGS:** \( 45.79 \times 7 = 320.53 \)
2. **VAT:** \( 5\% \times 320.53 = 16.03 \)
3. **Total:** \( 320.53 + 16.03 = 336.56 \)
4. **Gross Margin:** \( \frac{16.03}{336.56} = 0.0476 \approx 4.76\% \)

## Code

For the SQL queries used in this analysis, refer to the [SQL_queries.sql](https://github.com/Princekrampah/WalmartSalesAnalysis/blob/master/SQL_queries.sql) file.

```sql
-- Create database
CREATE DATABASE IF NOT EXISTS walmartSales;

-- Create table
CREATE TABLE IF NOT EXISTS sales(
	invoice_id VARCHAR(30) NOT NULL PRIMARY KEY,
    branch VARCHAR(5) NOT NULL,
    city VARCHAR(30) NOT NULL,
    customer_type VARCHAR(30) NOT NULL,
    gender VARCHAR(30) NOT NULL,
    product_line VARCHAR(100) NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    quantity INT NOT NULL,
    tax_pct FLOAT(6,4) NOT NULL,
    total DECIMAL(12, 4) NOT NULL,
    date DATETIME NOT NULL,
    time TIME NOT NULL,
    payment VARCHAR(15) NOT NULL,
    cogs DECIMAL(10,2) NOT NULL,
    gross_margin_pct FLOAT(11,9),
    gross_income DECIMAL(12, 4),
    rating FLOAT(2, 1)
);
```
