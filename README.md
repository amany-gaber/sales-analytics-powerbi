Sales ETL Pipeline & Dimensional Modeling
Project Overview

This project demonstrates an end-to-end ETL pipeline for sales data, starting from raw JSON extraction to building a clean, analytics-ready dimensional data model.
The final output supports reporting, trend analysis, and actual vs forecast comparison.

Project Objectives

Extract and validate raw sales data

Perform data profiling and quality checks

Apply transformations to improve consistency and usability

Build a dimensional model for analytical queries

Integrate forecast data for comparison with actual sales

Data Sources

Sales Data: Flattened JSON file containing transactional sales records

Forecast Data: Clean table covering years 2008–2009, aggregated by:

CountryRegion

Brand

Year

ETL Pipeline
1. Extract

Loaded flattened JSON sales data into a Pandas DataFrame

Applied UTF-8 encoding to avoid character issues

2. Validation & Profiling

Schema validation against predefined structure

Checked for:

Unexpected fields

Null values

Duplicate records

Key findings:

OrderDate was not in datetime format

High null ratios in customer-related attributes

Presence of duplicate records

3. Transformation

Standardized column names for consistency

Converted OrderDate to datetime format

Reviewed duplicate handling:

Duplicates were retained due to lack of a unique order identifier or timestamp

Removed low-value and redundant columns:

Education

Occupation

Color

CustomerCode

Retained CustomerKey as the primary customer identifier for performance and join efficiency

Data Modeling

The cleaned dataset was modeled using a Fact Constellation (Galaxy Schema) to support both transactional and forecast analysis.

Dimension Tables

dim_product
(ProductKey, ProductName, Brand, Subcategory, Category)

dim_customer
(CustomerKey, Name)

dim_geography
(GeographyKey, City, State, CountryRegion, Continent)

dim_date
(DateKey, OrderDate, Year, Month, MonthName, Quarter)

Fact Tables

fact_sales

Measures: Quantity, NetPrice, SalesAmount

forecast

Measures: Forecasted sales by region, brand, and year

Forecast Integration

Forecast data was validated and confirmed clean

Integrated to enable:

Actual vs forecast comparison

Trend analysis

Regional and brand-level insights

Output Files

The pipeline generates the following CSV files:

dim_product.csv

dim_customer.csv

dim_geography.csv

dim_date.csv

fact_sales.csv

forecast.csv

Key Design Decisions

Guest-mode customers are identified by geography-based codes, representing regions rather than individuals

Duplicate records were retained to avoid loss of valid same-day transactions

Integer surrogate keys were preferred for performance and scalability

Galaxy schema was chosen to support multiple fact tables sharing dimensions

Tools & Technologies

Python

Pandas

CSV-based data warehouse structure

Dimensional modeling (Star / Galaxy Schema)

Potential Enhancements

Introduce a unique order identifier or timestamp

Load data into a relational or cloud data warehouse

Add incremental ETL logic

Build dashboards for actual vs forecast analysis
