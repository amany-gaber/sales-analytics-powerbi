# Sales ETL Pipeline

An end-to-end ETL pipeline that transforms raw sales JSON data into an analytics-ready dimensional data model, enabling reporting and **actual vs forecast** analysis.

---

## Overview

This project focuses on data quality, transformation logic, and dimensional modeling, turning raw transactional data into a structure suitable for BI and analytical workloads.

---

## Data Sources

- **Sales Data**: Flattened JSON transactional dataset  
- **Forecast Data**: Clean forecast dataset (2008–2009) by country, brand, and year  

---

## ETL Flow



### Extract
- Loaded flattened JSON into Pandas
- Applied UTF-8 encoding

### Validate
- Schema validation (no unexpected fields)
- Null, duplicate, and data type checks
- Identified high null ratios in customer attributes
- Detected non-datetime `OrderDate`

### Transform
- Standardized column names
- Converted `OrderDate` to datetime
- Removed low-value and redundant columns:
  - `Education`
  - `Occupation`
  - `Color`
  - `CustomerCode`
- Duplicates were retained due to the absence of a unique order identifier

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

The forecast dataset was validated and integrated to support:
- Actual vs Forecast comparison
- Trend analysis
- Regional and brand-level insights

---

## Output Structure


---

## Key Design Decisions

- Guest customers are identified using geography-based codes (regional behavior)
- Integer surrogate keys were used for performance and efficient joins
- Galaxy schema was selected to support multiple analytical fact tables
- Data accuracy was prioritized over aggressive deduplication

---

## Tech Stack

- Python
- Pandas
- Dimensional Modeling
- CSV-based analytics layer

---

## Future Enhancements

- Introduce a unique order identifier or timestamp
- Load data into a data warehouse
- Build BI dashboards (Power BI / Tableau)
- Automate incremental ETL
