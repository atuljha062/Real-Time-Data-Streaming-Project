# Real Time Data Streaming Project

### Introduction
This project implements a real-time data pipeline for continuous data ingestion and transformation into a Snowflake data warehouse. It leverages various cloud technologies to achieve Change Data Capture (CDC) and Slowly Changing Dimensions (SCD) for historical data management.

### Architecture

### About Data
This project utilizes Faker to generate real-time data resembling customer records and stores them in CSV files within a designated folder on the EC2 instance. While the data provides a realistic simulation, it's for demonstration purposes only.

### Project Setup
This project requires the following services:

* **AWS**
  - EC2 Instance
  - S3 Bucket
* **Snowflake**
  - Data Warehouse
  - Snowpipe
  - Streams
  - Task
### Locally:

* Python with Faker library
  
### Technologies Used
1. **Docker:** Manages application deployment within the EC2 instance (Apache NiFi, Jupyter Notebook)

2. **Apache NiFi:** Automates data movement between systems
   
3. **Jupyter Notebook:** Used for data generation (with Faker in this project)
   
4. **Snowflake:** Cloud-based data warehouse for data storage and analysis
   
5. **Snowpipe:** Automatically ingests data from designated S3 buckets into Snowflake
    
6. **Snowflake Stored Procedure:** Reusable code block that executes MERGE and truncate commands

### Process Flow
1. **Data Generation (EC2):** Python scripts with Faker generate data and store it in a designated folder.
   
2. **Data Movement (Apache NiFi):** Apache NiFi monitors the folder and uploads newly created files to the designated S3 bucket.
   
3. **Data Ingestion (Snowpipe):** Snowpipe automatically ingests data from the S3 bucket into a staging table in Snowflake.
   
4. **Data Transformation (Snowflake Stored Procedure):** A scheduled task triggers the stored procedure every minute:
  * **MERGE Command (CDC):** Inserts, updates, or deletes data in the target table based on the staging table.
  * **Truncate Staging Table:** Prepares the staging table for the next batch of data.

5. **Historical Data Management (Snowflake Stream):** A Snowflake Stream captures changes to the actual table over time.
   
6. **SCD(Slowly Changing Dimension) Implementation:** The captured data populates a historical table designed with SCD techniques.

### Benefits
* **Real-time Data Pipeline:** Enables near real-time data updates in Snowflake.
* **Change Data Capture (CDC):** Ensures the target table reflects the latest data through inserts, updates, and deletes.
* **Slowly Changing Dimensions (SCD):** Maintains data integrity in the historical table through SCD techniques.
* **Scalability and Manageability:** Cloud-based technologies offer scalability for handling large data volumes.
