# Decathlon CLV Model

This repository contains the core notebooks developed for the Decathlon capstone project on predictive Customer Lifetime Value (CLV).

The project estimates future customer value by combining:
- a frequency prediction model to estimate expected future purchases,
- a monetary conversion step to translate predicted purchases into expected revenue,
- and a tier-level analysis to identify the key behavioral drivers associated with higher-value customers.

## Key Results

- **Best-performing model:** Gradient Boosted Trees with enhanced features, achieving **RMSE = 3.55** and **MAE = 2.11** on the validation set.
- **Ranking quality:** The best model achieved **Spearman correlation = 0.620** and **Top-decile lift = 3.24x**, indicating strong targeting power for high-value customers.
- **Scored customer base:** The final December 2024 snapshot includes **217,665 customers**.
- **Predicted portfolio value:** Total projected **3-year CLV = EUR 82.56M** across the scored customer base.

## Repository Structure

### 1. `CLV_Frequency_Modeling.ipynb`
Builds the predictive model for future purchase frequency.

This notebook:
- prepares the modeling dataset,
- defines the feature sets,
- applies a time-based train-validation split,
- trains and compares multiple regression models,
- evaluates predictive performance,
- and saves frequency predictions and model metrics for downstream use.

### 2. `CLV_Monetary_Conversion.ipynb`
Transforms predicted purchase frequency into projected revenue and CLV.

This notebook:
- loads the selected frequency predictions,
- computes a historical global Average Order Value (AOV),
- estimates expected 12-month revenue,
- converts annual value into projected 3-year CLV,
- and creates final customer-level output tables for downstream business use.

### 3. `Tier_Driver_Analysis.ipynb`
Analyzes customer segments and the behavioral drivers associated with each value tier.

This notebook:
- segments customers into CLV tiers,
- compares driver prevalence across tiers,
- identifies the strongest differentiators of high-value customers,
- and supports business interpretation and targeting recommendations.

## Project Logic

The pipeline follows a simple business logic:

1. Predict how often each customer is expected to purchase in the next 12 months.
2. Convert predicted frequency into expected revenue using a historical AOV.
3. Project longer-term CLV from expected annual value.
4. Analyze which customer behaviors are most associated with higher-value tiers.

## Modeling Overview

The frequency modeling stage compares four models:
- Linear Regression (drivers-only)
- Gradient Boosted Trees (drivers-only)
- Linear Regression (enhanced)
- Gradient Boosted Trees (enhanced)

The enhanced feature set combines behavioral drivers with baseline customer controls such as historical frequency, recency, and tenure.  
The best-performing model was **Gradient Boosted Trees with enhanced features**.

## Execution Order

Run the notebooks in the following order:

1. `CLV_Frequency_Modeling.ipynb`
2. `CLV_Monetary_Conversion.ipynb`
3. `Tier_Driver_Analysis.ipynb`

## Environment

This project was developed in **Databricks using PySpark**.

## Data Access and Confidentiality

The notebooks rely on Decathlon internal tables and intermediate Databricks outputs that are not included in this repository.

For confidentiality reasons, this repository is intended to document:
- the modeling approach,
- the analytical workflow,
- and the business logic behind the CLV pipeline,

rather than provide full external reproducibility with raw data.

## Notes

- Source data exports are not included.
- Upstream internal table construction and raw data preparation steps are maintained separately.
- This repository focuses on the final modeling and analytical workflow used for the capstone deliverable.

## Business Relevance

The final output is a customer-level projected CLV estimate that can support:
- customer prioritization,
- retention and acquisition decision-making,
- value-based segmentation,
- and identification of the behaviors most strongly associated with long-term value.

## Team

This project was developed as part of the Decathlon capstone by:

- Laura Barros
- Oscar Ricardo Moreno
- Regina Ortega
- Jim Vincent
- Teresita Alessandri
