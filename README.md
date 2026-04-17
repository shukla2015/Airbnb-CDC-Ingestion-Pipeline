# Airbnb-CDC-Ingestion-Pipeline
Project Overview

This project implements an end-to-end data pipeline simulating an Airbnb booking system. It integrates batch and real-time processing using Azure services, combining SCD Type-1 transformations and CDC-based ingestion into a unified data warehouse solution.

# Tech Stack
Python
Azure Data Factory (ADF)
Azure Synapse Analytics
Azure Data Lake Storage (ADLS)
MongoDB
SQL (Stored Procedures, MERGE)

# Pipeline Architecture
# Pipeline 1: Customer Data Processing (Batch - SCD Type 1)
Source: CSV files stored in ADLS
ADF reads and processes customer data
Implements SCD Type-1 logic (overwrite existing records)
Loads transformed data into Synapse Customer Table

# Pipeline 2: Booking Data Processing (CDC - Real-time Simulation)
Source: MongoDB collection (booking events)
ADF ingests incremental data (CDC logic)
Performs upsert (MERGE) into Synapse Booking Table
Executes stored procedure for post-processing / business logic

# Pipeline 3: Orchestration Pipeline
Parent pipeline controlling Pipeline 1 and Pipeline 2
Implements:
Sequential execution
Dependency chaining
Trigger-based scheduling

# Key Features
✅ Hybrid pipeline design (Batch + CDC)
✅ SCD Type-1 implementation for dimension table
✅ Upsert logic using MERGE for fact table
✅ Automated workflow orchestration using ADF
✅ Integration of multiple data sources (ADLS + MongoDB)
✅ Modular and scalable architecture
📊 Data Flow
Customer CSV files → ADLS
ADF Pipeline 1 → SCD1 → Synapse (Customer Table)
MongoDB Booking Data → ADF Pipeline 2 → Upsert → Synapse (Booking Table)
Stored Procedure Execution → Final transformations
Pipeline 3 orchestrates entire workflow


Author
Shashank Shukla
Data Engineering 
