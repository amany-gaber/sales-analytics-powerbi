# Sales ETL Pipeline

An end-to-end **ETL pipeline** that transforms raw sales JSON data into an **analytics-ready dimensional data model**, enabling reporting and **Actual vs Forecast** analysis.

---

## Overview

This project focuses on **data quality, transformation logic, and dimensional modeling**, converting raw transactional data into a structure suitable for **BI and analytical workloads**.

The pipeline supports:
- Historical sales analysis (2008–2009)
- Actual vs Forecast comparison
- Regional, product, and category-level insights

---

## Data Sources

- **Sales Data**
  - Flattened JSON transactional dataset
  - Contains order, product, customer, and geographic attributes

- **Forecast Data**
  - Clean forecast dataset
  - Covers **2008–2009**
  - Granularity: Country, Brand, Year

---

## ETL Flow

### Extract
- Loaded flattened JSON files into **Pandas**
- Applied **UTF-8 encoding** to ensure text consistency

### Validate
- Schema validation (no unexpected fields)
- Null value checks
- Duplicate checks
- Data type validation
- Identified:
  - High null ratios in customer attributes
  - Non-datetime `OrderDate` field

### Transform
- Standardized column names
- Converted `OrderDate` to datetime
- Removed low-value or redundant columns:
  - `Education`
  - `Occupation`
  - `Color`
  - `CustomerCode`
- Duplicates were **retained** due to the absence of a unique order identifier

---

## Data Model

The final design follows a **Fact Constellation (Galaxy Schema)**, allowing multiple fact tables to share common dimensions.

### Dimensions

| Dimension | Description |
|---------|------------|
| dim_product | Product attributes and hierarchy |
| dim_customer | Customer master data |
| dim_geography | Geographic hierarchy |
| dim_date | Calendar attributes |

### Fact Tables

| Fact Table | Description |
|-----------|------------|
| fact_sales | Transactional sales data |
| forecast | Forecasted sales values |

---

## Forecast Integration

The forecast dataset was validated and integrated to enable:
- Actual vs Forecast comparison
- Trend analysis
- Regional and brand-level insights
- Performance gap analysis

---

## Business Insights

### Overall Performance (Global)
- **Total Sales:** **$42.64M**
- **Year-over-Year decline:**
  - 2008: **$23.1M**
  - 2009: **$19.55M**
  - **YoY Growth:** **–15.38%**
- The decline is **structural**, not seasonal, and visible across most markets and categories.

---

### United States
**Largest market, but declining**
- **Total Sales:** **$34.33M**
- **YoY Growth:** **–18.72%**
- **Top Categories:**
  - Home Appliances (largest contributor)
  - Computers
  - Cameras & Camcorders

**Key Insights**
- Heavy reliance on Home Appliances makes the US market **highly sensitive to economic slowdowns**
- 2009 sales **underperformed 2008** in most months

---

### Germany
**Small market with the sharpest decline**
- **Total Sales:** **$6.24M**
- **YoY Growth:** **–49.56%**
- Actual sales in 2009 were **significantly below forecast**

**Key Insights**
- Germany represents a **strategic weakness**
- Requires pricing adjustments, cost optimization, or reduced investment

---

### China
**Emerging market with strong potential**
- **Total Sales:** **$2.07M**
- 2009 Sales ≈ **$2.06M**
- Extremely high YoY growth (inflated due to very low 2008 base)

**Key Insights**
- Strong demand in **Home Appliances** and **Computers**
- Market is in an **early growth phase**, not saturation

---

### Product Performance
- **Best-Selling Products:**
  - Washers & Dryers
  - Refrigerators
- Sales are **highly concentrated** in the top 10 products

**Risk**
- Overdependence on a limited product set increases **revenue volatility**

---

### Forecast vs Actual (2009)
- Actual sales **missed forecasts in all regions**
- Largest gaps observed in:
  - United States
  - Germany

**Key Insight**
- Forecasting models were **overly optimistic** and did not fully account for market contraction

---

### Monthly Sales Trends
- **2008:** Strong peaks in **Q2 and Q3**
- **2009:** Lower peaks and weaker momentum, especially in **Q4**

**Seasonality Insight**
- Best-performing periods remain **Q2–Q3**
- End-of-year performance weakened in 2009

---

## Recommendations

1. Reduce exposure to **Germany** or re-evaluate go-to-market strategy
2. Increase investment in **China** (marketing, distribution, product expansion)
3. Diversify the **product portfolio** to reduce concentration risk
4. Rebuild **forecasting models** with conservative economic assumptions
5. Focus sales and marketing campaigns around **Q2–Q3**, where demand is strongest

---

## Key Design Decisions

- Guest customers are identified using geography-based codes
- Integer **surrogate keys** were used for performance and efficient joins
- Galaxy schema selected to support multiple analytical fact tables
- Data accuracy prioritized over aggressive deduplication

---

## Tech Stack

- Python
- Pandas
- Dimensional Modeling
- CSV-based analytics layer

---

## Future Enhancements

- Introduce a unique order identifier or timestamp
- Load data into a data warehouse (Snowflake / BigQuery / Redshift)
- Build BI dashboards (Power BI / Tableau)
- Automate incremental ETL pipelines

---
