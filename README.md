# 📈 Demand Planning Project

A demand forecasting project developed for **NorthStar Retail** to improve inventory planning by forecasting weekly SKU-level demand using multiple time-series forecasting techniques. The project evaluates forecasting accuracy using industry-standard metrics and generates actionable 12-week forecasts to support replenishment decisions.

---

# Table of Contents

- [Project Introduction](#project-introduction)
  - [Background](#background)
  - [Problem Statement](#problem-statement)
  - [Objective](#objective)
  - [My Role as a Demand Planner](#my-role-as-a-demand-planner)
  - [Approach](#approach)
  - [Business Value](#business-value)
- [Methodology](#methodology)
  - [Data](#data)
  - [Tools Used](#tools-used)
  - [Data Cleaning and Exploration](#data-cleaning-and-exploration)
    - [Duplicates](#duplicates)
    - [Missing Values](#missing-values)
    - [Outlier Analysis](#outlier-analysis)
    - [Data Types](#data-types)
    - [Weekly Aggregation and Table Integration](#weekly-aggregation-and-table-integration)
- [Forecasting Methodology](#forecasting-methodology)
  - [Exponential Smoothing (ES)](#exponential-smoothing-es)
  - [Moving Average (MA)](#moving-average-ma)
  - [Weighted Moving Average (WMA)](#weighted-moving-average-wma)
- [Forecast Accuracy Evaluation](#forecast-accuracy-evaluation)
  - [Mean Absolute Deviation (MAD)](#mean-absolute-deviation-mad)
  - [Mean Absolute Percentage Error (MAPE)](#mean-absolute-percentage-error-mape)
  - [Root Mean Squared Error (RMSE)](#root-mean-squared-error-rmse)
  - [Forecast Bias](#forecast-bias)
- [Forecast Model Selection](#forecast-model-selection)
- [Forecast Results](#forecast-results)
- [Forecast Bias Analysis](#forecast-bias-analysis)
- [Recommendations](#recommendations)
- [Conclusion](#conclusion)

---

# Project Introduction

## Background

NorthStar Retail operates in a dynamic retail environment where demand for products varies across time, stores, and SKUs. Accurate demand forecasting is critical to ensure that the right products are available at the right time while minimizing excess inventory. However, the company currently faces significant uncertainty in weekly SKU-level demand, making it difficult to plan inventory and replenishment effectively.

Without a structured forecasting approach, decisions are often based on historical averages or intuition, which do not adequately capture demand variability or external factors such as promotional activity. This has led to operational challenges, including frequent stockouts that result in lost sales and customer dissatisfaction, as well as overstocking that increases holding costs and reduces profitability.

---

## Problem Statement

The core business problem is the lack of a reliable and data-driven method to forecast short-term demand at the SKU level. This uncertainty limits the company’s ability to make informed inventory decisions and increases exposure to both stockout and overstock risks.

---

## Objective

The objective of this project is to develop and evaluate forecasting models capable of accurately estimating weekly demand for individual SKUs over a 12-week planning horizon.

Specifically, the project aims to:

- Build baseline forecasting models using:
  - Moving Average (MA)
  - Weighted Moving Average (WMA)
  - Exponential Smoothing (ES)
- Incorporate external demand drivers, such as promotional activity, using regression analysis.
- Evaluate forecasting performance using:
  - Mean Absolute Percentage Error (MAPE)
  - Mean Absolute Deviation (MAD)
  - Root Mean Squared Error (RMSE)
  - Forecast Bias
- Select the most appropriate forecasting model for each SKU.
- Generate actionable 12-week forecasts to support inventory planning.

---

## My Role as a Demand Planner

NorthStar Retail contracted me to strengthen its demand planning function by analyzing historical SKU-level sales data and developing a reliable forecasting framework to improve inventory and replenishment decisions.

My responsibilities included:

- Analyzing historical demand patterns.
- Evaluating multiple forecasting techniques.
- Selecting the most appropriate forecasting model for each SKU.
- Generating 12-week demand forecasts for operational planning.
- Assessing the impact of promotional activities on product demand.
- Providing data-driven recommendations to improve forecasting accuracy, inventory availability, and overall supply chain efficiency.

---

## Approach

The project followed a structured analytical workflow beginning with data cleaning and transformation, followed by exploratory data analysis to understand historical demand patterns.

Forecasting models were then developed using the complete historical dataset. Their performance was evaluated using in-sample forecasting accuracy metrics, including MAD, MAPE, RMSE, and Forecast Bias. The best-performing model was selected for each SKU and used to generate 12-week demand forecasts.

The final stage focused on interpreting the forecasting results to derive actionable insights relating to demand stability, forecasting reliability, and inventory planning risk.

---

## Business Value

Implementing a structured forecasting framework enables NorthStar Retail to improve inventory planning by reducing demand uncertainty and supporting more informed operational decisions.

The resulting forecasts provide a foundation for:

- Optimizing inventory replenishment.
- Reducing stockouts.
- Minimizing excess inventory and carrying costs.
- Improving short-term operational planning.
- Understanding the impact of promotional activities on demand.
- Supporting more effective marketing and inventory strategies.

  # Methodology

## Data

This project was conducted using a fictitious dataset created to simulate the operations of **NorthStar Retail**, a fictional retail company. The data was structured within a relational database environment and designed to reflect realistic retail demand planning scenarios across multiple stores and products over a two-year period.

Core tables included daily sales transactions, promotional activity, pricing data, and daily demand from **2024 to 2025**. Supporting dimension tables provided descriptive information for dates, products, and store locations.

The dataset contained key variables including transaction dates, SKU identifiers, store identifiers, units sold, pricing, revenue, and promotion details, creating a realistic foundation for forecasting weekly demand and analyzing the impact of promotional activity.

For the purpose of this project, only data from **Store 1** and **five SKUs (products)** were analysed.

### Data Dictionary

| Table | Variable | Type | Description |
|--------|----------|------|-------------|
| **fact_sales_daily** (contains daily sales data) | `store_id` | Nominal | Unique identifier used to distinguish each retail store location. |
| | `sku_id` | Nominal | Unique identifier used to distinguish each product or stock keeping unit. |
| | `units_sold` | Discrete | Number of product units sold per day. |
| **dim_calendar** | `week_start` | Interval | Date of sale. |

---

## Tools Used

The analysis was conducted using **MySQL** for data storage, querying, joins, and transformation of raw transactional data into structured forecasting datasets.

**Microsoft Excel** was used for exploratory analysis, forecasting model development, and performance evaluation using metrics such as **MAPE**, **MAD**, **RMSE**, and **Bias**. Excel was also used to create charts, compare forecasting methods, and generate final 12-week demand forecasts.

Together, these tools provided an efficient workflow for data preparation, analysis, and decision-support reporting.

---

## Data Cleaning and Exploration

Data was imported into **MySQL** for cleaning and exploration to derive final relevant columns for analyses.

Cleaning procedures included:

- Checking for duplicates
- Checking for null values
- Outlier analysis
- Data type validation

---

### Duplicates

Duplicate validation checks were performed on both the **fact_sales_daily** and **dim_calendar** tables to ensure the integrity and uniqueness of records prior to analysis.

For the **fact_sales_daily** table, records were grouped by **sku_id**, **date**, **store_id**, and **units_sold** to identify repeated sales transactions that could distort demand calculations and forecasting results.

Similarly, the **dim_calendar** table was checked by grouping records using **date** and **week_start** to verify that each calendar date was uniquely mapped to a single weekly period.

Any grouping with a count greater than one was treated as a potential duplicate.

No duplicate records were identified in either table.

![Duplicate Validation Results](images/duplicate-validation-results.png)

---

### Missing Values

Null value validation was performed on the **fact_sales_daily** and **dim_calendar** tables to verify that all essential fields contained valid data before analysis began.

Within the **fact_sales_daily** table, checks were carried out on **sku_id**, **date**, **store_id**, and **units_sold** to ensure that no sales observations were missing key transactional information.

The **dim_calendar** table was also reviewed for missing entries in the **date** and **week_start** fields to confirm accurate time mapping for weekly aggregation and forecasting activities.

Performing these validations helped ensure the reliability and usability of the dataset for subsequent analytical processes.

No missing values were found for both tables.

![Missing Value Validation](images/missing-value-validation.png)

---

### Outlier Analysis

A boxplot analysis was conducted on weekly sales values to identify potential outliers and assess the variability of demand.

The visualization showed that most weekly sales observations were concentrated within the interquartile range, with a median demand level of approximately **139 units** and an average of about **138 units**.

However, several unusually high sales observations were identified above the upper whisker, with values ranging from approximately **224 to 246 units**, while one unusually low observation was detected around **31 units**.

These outliers indicate periods of abnormal demand behavior that may have been influenced by factors such as promotional activity, temporary demand spikes, or operational disruptions, and are not likely to have been caused by data errors.

![Weekly Sales Boxplot](images/weekly-sales-boxplot.png)

---

### Data Types

Data type checks were conducted on the key variables used in the forecasting analysis to ensure they were stored in formats appropriate for aggregation and modeling.

Variables such as **sku_id** and **store_id** were stored as text fields to serve as categorical identifiers, while **units_sold** was stored as a numeric field to support quantitative analysis.

In the **dim_calendar** table, **date** and **week_start** were validated as temporal fields used for weekly aggregation and time-based forecasting activities.

![Data Type Validation](images/data-type-validation.png)

---

### Weekly Aggregation and Table Integration

To prepare the dataset for forecasting analysis, the **fact_sales_daily** table was joined with the **dim_calendar** table using the shared **date** field.

This integration allowed each daily sales transaction to be mapped to its corresponding weekly period through the **week_start** variable.

Following the join, sales data was aggregated to the weekly level by grouping records according to **week_start**, **store_id**, and **sku_id**, while summing the **units_sold** field to generate total weekly demand per product and store.

This process transformed the raw transactional data into a structured weekly demand dataset suitable for time-series forecasting and comparative model analysis.

![Weekly Aggregation and Table Integration](images/weekly-aggregation-and-table-integration.png)

---
