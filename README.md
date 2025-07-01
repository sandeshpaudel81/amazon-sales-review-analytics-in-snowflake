# Amazon Sales Review Analytics in Snowflake

This project demonstrates how to design and build a scalable data warehouse in **Snowflake** using a raw e-commerce dataset from **Kaggle**. The dataset includes product information, category hierarchies, pricing details, user reviews, and ratings.

The project includes:
- Data ingestion
- Data cleaning and transformation
- Star schema modeling
- Fact and dimension tables
- Analytical queries for business insights

---

## Project Overview

**Goal:** Analyze Amazon product reviews and ratings using a dimensional model in Snowflake.

**Dataset:** [Amazon Sales Dataset (Kaggle)](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset/)

**Key Objectives:**
- Clean and standardize product and review data
- Build star schema with fact and dimension tables
- Run analytical queries to uncover insights like:
  - Top-reviewed products
  - Highest-rated products
  - Most active reviewers
  - Category-based performance

---

## Schema Design

### Raw Schema (`raw`)
Stores the raw ingested CSV data:
- `raw.amazon_sales`: The source table containing all columns as strings

### Analytics Schema (`analytics`)
Transformed data organized into a **star schema**:
- `fact_review`: Fact table with one row per unique user review
- `dim_product`: Dimension table with cleaned product metadata

---

## Data Cleaning

- Removed ₹, %, and commas from price and rating fields
- Converted data types: prices (FLOAT), ratings (FLOAT), review count (INT)
- Split hierarchical category strings into up to 5 levels
- Exploded multi-user/multi-review rows into individual review rows using `ARRAY_GET` and `SEQUENCE`
- Deduplicated reviews and products (e.g., duplicate `review_id` or `product_id` with minor variations)

---

## Star Schema 

dim_product <---------- fact_review
                            |
                            |
                            |
                            |
                        dim_user
