# 2022 Airlines Departure Data Lakehouse

A batch lakehouse built on 2022 US domestic airline departure data, implementing a Medallion architecture (bronze → silver → gold) with Delta Lake on Databricks.

## 📌 Overview

This project ingest the raw flight departure records from the landingzone and refines them to clea, analytics ready star schema. The final goal of this project is to support efficient querying, reporting, and analytics for airline departure operations and performance metrics.

Key Features:
- Dimensional database modelling (star schema).
- Medallion Architecture (Bronze->Silver->Gold)
- Incremental batch loading using merge to demostrate upserts
- Orchestrated as scheduled Lakeflow jobs
- Delta Lake

## Data Source

The project is using [2022 US Airlines Domestic Departure dataset ](https://www.kaggle.com/datasets/jl8771/2022-us-airlines-domestic-departure-data).

The main CompleteData.csv file has been divide up to monthly datasets to simulate incremental data loading. Each monthly batch has been assigned to a batch_id (ex.: 2022-1) and I used this batch_id to orchestrate the pipeline. 

## 🧱 Architecture

### Bronze Layer

- Ingests the raw datasets into Delta tables, matched against an explicit schema.
- Adds batch_id, ingestion_timestamp, source_file columns for auditing and data lineage.
- No transformations applied to the data

### Silver Layer

- Performs quality check through a custom written SparkQCheck class. 
- Cleans data (removes duplicates and drops columns with excessive missing values).
- Incremental data batch loading using MERGE.
- Renames columns for consistency and clarity.

### Gold Layer

- Star schema optimized for analytics.
    - Fact table -> fact_flights: one row per flight for metrics and foreing keys to each dimensions.
    - Dimension tables:
        - dim_aircrafts -> Aircraft information separated from the main table.
        - dim_airlines  -> Airlines information dimension table.
        - dim_airports  ->


## 🗃️ ERD Diagram


## 🧰 Tech Stack

- **Databricks Communnity Edition**
- **Pyspark**
- **Delta Lake**
- **SQL**


## 📁 Repository Structure


## 🔗 References

- Kaggle - 2022 US Airlines Domestic Departure Data
  https://www.kaggle.com/datasets/jl8771/2022-us-airlines-domestic-departure-data

✅ This project uses only publicly available data for educational purposes.
