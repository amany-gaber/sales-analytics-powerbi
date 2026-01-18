# Sales ETL Pipeline & Analytics Data Model

An end-to-end Sales ETL pipeline that transforms raw JSON data into an analytics-ready dimensional data model, enabling reporting, trend analysis, and actual vs forecast comparison.

## Why This Project?

This project focuses on data quality, modeling decisions, and analytics readiness, not just data cleaning.

It demonstrates how raw transactional data can be transformed into a scalable analytical structure suitable for BI and reporting use cases.

## Dataset Overview

Sales Data: Flattened JSON transactional dataset

Forecast Data: Clean forecast table for 2008–2009

Data granularity: Order-level transactions

## ⚙️ ETL Pipeline Overview
Extract  →  Validate  →  Transform  →  Model  →  Analyze

🔹 Extract

Loaded flattened JSON into Pandas DataFrame

UTF-8 encoding applied

🔹 Validate & Profile

Schema validation (no unmapped fields)

Null, duplicate, and data type checks

Identified:

High null ratios in customer attributes

Date stored without proper datetime type

🔹 Transform

Standardized column names

Converted OrderDate to datetime

Removed redundant / low-value columns:

Education, Occupation, Color, CustomerCode

Duplicates retained intentionally due to missing unique order identifier

🏗️ Data Modeling

The final model follows a Fact Constellation (Galaxy Schema) to support both transactional and forecast analysis.

⭐ Dimensions
Dimension	Description
dim_product	Product hierarchy and attributes
dim_customer	Customer master data
dim_geography	Location hierarchy
dim_date	Calendar attributes
🔢 Fact Tables
Fact Table	Description
fact_sales	Transactional sales data
forecast	Planned / forecasted sales
🔮 Forecast Integration

Forecast data validated and integrated

Enables:

Actual vs Forecast analysis

Trend analysis

Regional and brand-level insights

📂 Project Output
├── dim_product.csv
├── dim_customer.csv
├── dim_geography.csv
├── dim_date.csv
├── fact_sales.csv
├── forecast.csv

🧩 Key Design Decisions

Guest customers are identified via geography-based codes (regional behavior)

Integer surrogate keys used for performance and scalability

Galaxy schema chosen to support multiple fact tables

Data accuracy prioritized over aggressive deduplication

🛠️ Tech Stack

Python

Pandas

Dimensional Modeling (Star / Galaxy Schema)

CSV-based analytics layer

🚀 Future Improvements

Add unique order identifier or timestamp

Load data into a cloud data warehouse

Build BI dashboards (Power BI / Tableau)

Automate incremental ETL
