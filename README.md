# Airbnb-CDC-Ingestion-Pipeline
Project Overview

This project simulates an end-to-end data engineering pipeline for an Airbnb-like booking system. It combines batch and CDC-based ingestion to process customer and booking data into a cloud data warehouse using Azure services.

# Tech Stack
Python
Azure Data Factory (ADF)
Azure Synapse Analytics (Dedicated SQL pool)
Azure Data Lake Storage Gen 2 (ADLS)
MongoDB
SQL (Stored Procedures, MERGE)

# Architecture

# Data Sources
Customer data (CSV files) stored in ADLS Gen2
Booking data generated via Python (Faker) and stored in MongoDB
# Data Warehouse
In Azure Synapse 2 tables
customer_dim → Dimension table (SCD Type-1)
bookings_fact → Fact table (CDC-based upsert)

# Pipeline Architecture
# Pipeline 1: LoadCustomerDim (Batch Processing - SCD Type 1)
Reads CSV files from ADLS (customer_raw_data)
In ADF Uses Get Metadata + ForEach activities to process multiple files
Loads data into Synapse customer_dim table with SCD Type-1 logic
Moves processed files to customer_archive folder

# Pipeline 2: LoadBookingFact (CDC Processing - Real-time Simulation)
Reads booking data incrementally from MongoDB (CDC logic)
Applies transformations and performs UPSERT (MERGE) into bookings_fact
Executes stored procedure in Synapse for aggregated table creation

# Pipeline 3: AirBnBCDCPipeline (Orchestration)
Parent pipeline orchestrating:
LoadCustomerDim
LoadBookingFact
Ensures sequential execution, Dependency chaining and Trigger-based scheduling

# Data Flow
Python → MongoDB → ADF (CDC) → Synapse (Fact Table)
ADLS CSV → ADF (Batch) → Synapse (Dim Table)
→ Stored Procedure → Aggregated Table

# Key Features
Hybrid pipeline (Batch + Realtime + CDC)
SCD Type-1 implementation for dimension data
Upsert logic for fact table using MERGE
Automated file archival in ADLS
Pipeline orchestration with dependency chaining

# Use Cases
Real-time booking analytics
Incremental data ingestion design
Data warehouse modeling (Dim + Fact)

# Key Learnings
Implementing CDC pipelines using MongoDB
Designing SCD Type-1 logic in Synapse
Building modular ADF pipelines
Handling batch + streaming data together

# Author
Shashank Shukla
