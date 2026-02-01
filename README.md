# Medallion Architecture for Retail Data in Databricks

## Overview

This project implements a **Medallion Architecture** on Databricks to transform retail data from CRM and ERP systems into a high-performance Star Schema for analytics.

## Technical Architecture

- **Bronze (Raw)**  
  Ingest CSV files from `datasets/` into Delta tables using Python notebooks.

- **Silver (Cleansed)**  
  Cleanse and standardize data using Python notebooks, applying validation and transformation logic.

- **Gold (Curated)**  
  Build a Star Schema optimized for BI using Python notebooks:
  - **dim_customers & dim_products**: cleaned, unique dimensions with surrogate keys  
  - **fact_sales**: consolidated transactional fact table with referential integrity

- **Shared Components**
  - **helpers/**: Bronze and Silver engines to avoid duplicated logic across notebooks  
  - **tests/**: folder with 8 automated data quality checks validating Gold layer


### Data Platform Architecture

![Architecture](./images/architecture.gif)

## Engineering Highlights

- **Automated Orchestration**: Managed via `run_all_pipeline.ipynb` using `%run` (Databricks Free Edition limitation).  
- **Data Quality**: Eight tests ensure clean, consistent, and reliable data across all layers. 
- **Idempotency**: Safe to rerun without duplicating data.  
- **Error Handling**: Missing category links mapped to 'Unknown' to prevent data loss.  

## 📈 Data Model (Star Schema)

Visual representation of the Gold Zone:

```mermaid
erDiagram
    fact_sales }|--|| dim_customers : "customer_key"
    fact_sales }|--|| dim_products : "product_key"

    fact_sales {
        string order_number
        int customer_key
        int product_key
        date order_date
        date ship_date
        date due_date
        int quantity
        double price
        int sales_amount
        timestamp gold_ingestion_ts
    }

    dim_customers {
        int customer_key
        int customer_id
        string customer_number
        string first_name
        string last_name
        string country
        string marital_status
        string gender
        date birthdate
        date create_date
        timestamp gold_ingestion_ts
    }

    dim_products {
        int product_key
        int product_id
        string product_number
        string product_name
        string category_id
        string category
        string subcategory
        boolean maintenance_flag
        string product_line
        int product_cost
        date start_date
        timestamp gold_ingestion_ts
    }
```

## How to Run
For detailed, step-by-step instructions please see the:  
➡️ [Setup Guide](./SETUP_GUIDE.md)



