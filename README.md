# Decathlon Spain — CLV Prediction Model

Predictive Customer Lifetime Value (CLV) pipeline for Decathlon Spain members, built on Databricks using PySpark. This project trains behavioral models to predict future purchase frequency, converts predictions into monetary CLV, segments customers into actionable tiers, and analyzes the key behavioral drivers behind each tier.

## Notebooks

### 1. `CLV_Frequency_Modeling.ipynb`
Trains and evaluates four predictive models for customer purchase frequency:
- **Linear Regression (Drivers-Only):** 9 behavioral engagement features
- **GBT (Drivers-Only):** Gradient Boosted Trees with the same 9 features
- **Linear Regression (Enhanced):** Adds log-transformed baseline controls (past frequency, recency, tenure)
- **GBT (Enhanced):** Full feature set with Gradient Boosted Trees

**Behavioral drivers used:** omnichannel activity, contactability, UMP membership, multi-category shopping, fast second purchase, recency, ecosystem engagement, app usage, and return behavior.

### 2. `CLV_Monetary_Conversion.ipynb`
Converts predicted frequency into monetary CLV and segments customers into tiers:
- Computes global Average Order Value (AOV) per snapshot date (365-day lookback, anti-leakage)
- Converts predicted frequency to 12-month GMV to 3-year CLV in EUR
- Segments customers into **Platinum / Gold / Silver / Bronze** tiers
- Compares behavioral-predictive CLV vs. Decathlon's historical-linear CLV

### 3. `Tier_Driver_Analysis.ipynb`
Analyzes behavioral driver prevalence across CLV tiers:
- Tier distribution overview (customer count, value concentration)
- Driver adoption rates by tier (high-value vs. low-value comparison)
- Gap analysis identifying targeting opportunities for campaign strategy

## Key Results

| Tier | CLV Threshold | % of Customers | % of Total CLV |
|------|--------------|----------------|----------------|
| Platinum | >= 1,000 EUR | 7.0% | 28.4% |
| Gold | 500-999 EUR | 16.3% | 29.8% |
| Silver | 200-499 EUR | 33.7% | 28.3% |
| Bronze | 50-199 EUR | 43.0% | 13.6% |

- **Top 23% of customers (Platinum + Gold) drive 58% of total CLV**
- **13x value concentration** between Platinum (avg 1,546 EUR) and Bronze (avg 121 EUR)
- Top differentiating drivers: multi-category shopping, recent purchase activity, and app usage

## Tech Stack

- **Platform:** Databricks (PySpark)
- **Models:** Linear Regression, Gradient Boosted Trees (PySpark ML)
- **Data:** Decathlon Spain transactional + member engagement data
- **Visualization:** Matplotlib

## Author

Laura Vale Barros — [GitHub](https://github.com/lauravalebarros)
