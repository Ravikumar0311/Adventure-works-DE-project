# Adventure-works-DE-project
A complete Azure Data Engineering pipeline using the AdventureWorks dataset, implementing ***Medallion Architecture*** (Bronze, Silver, Gold layers), ***PySpark in Azure Databricks***, ***Azure Data Factory (ADF)*** for orchestration, ***Azure Data Lake Gen2*** for storage, ***Azure Synapse*** for analytical modeling, and ***Power BI*** for data visualization.

# Project Objective
The goal of this project is to simulate a real-time data engineering and analytics pipeline for a retail business using Azure-native tools and services. It helps demonstrate:
- Ingestion of raw enterprise data from external sources
- Transformation and cleansing using scalable compute (Databricks)
- Storage in structured, query-optimized formats
- Delivery of insights through visualization tools

# Tools & Technologies Used
**Programming**: 
- Python
- SQL

**Services**:
- Azure Data Factory (ADF)
- Azure Data Lake Storage Gen2
- Azure Databricks (PySpark)
- Azure Synapse Analytics (Dedicated Pool/SQL)
- Power BI

# Architecture Overview
The project follows a Medallion Architecture:

1) **Bronze Layer** – Raw Ingestion
- Raw CSV files from AdventureWorks are ingested using Azure Data Factory into ADLS Gen2 (Raw container).
- No transformation or validation is done in this layer.
- Serves as a data backup and audit log.

2) **Silver Layer** – Cleansed & Transformed
- PySpark transformations are performed in Azure Databricks.
- Cleaning, standardization, null handling, and schema enforcement are done here.
- Data is written back to ADLS Gen2 (Cleansed container) in parquet format.

3) **Gold Layer** – Aggregated & Modeled
- Data from the Silver layer is aggregated and joined to form business-friendly dimensional models (facts and dimensions).
- Final tables are written to Azure Synapse Analytics using PolyBase or Azure SQL scripts.
- These are used as the source for Power BI dashboards.

# Key Transformations in Databricks
- Ingestion of CSV Files from Bronze Layer (Raw).
- Added Month and Year columns extracted from the Date column.
- Created a full name column by concatenating multiple name fields.
- Extracted meaningful substrings from ProductSKU and ProductName fields.
- Converted StockDate to timestamp format.
- Standardized OrderNumber by replacing prefix ‘S’ with ‘T’.

# How to Run the Project
1. **Upload Data**
- Upload CSV files into raw container in ADLS Gen2.

2. **Configure ADF**
- Import pipeline JSONs from adf
- Set up linked services (Blob storage, Databricks, Synapse)

3. **Run Databricks Notebook**
- Load and execute /notebooks/databricks_transform.ipynb
- Transformed Parquet files go to the silver/ and gold/ containers

4. **Load into Synapse**
- Execute SQL scripts in /sql/ to create tables and views

# Business Value Delivered
- Near real-time data insights
- Unified customer and sales analytics
- Improved decision-making through modern dashboards
- Foundation for future ML/AI models using structured data layers

# License
This project is released under the MIT License. You are free to use, distribute, and modify for personal or commercial use.
