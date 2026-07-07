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
