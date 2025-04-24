# Flight Booking Data Processing Pipeline

## Overview

This project implements an automated data pipeline for processing and analyzing flight booking data. The pipeline ingests raw CSV data, performs transformations using Apache Spark, and loads the results into BigQuery tables for analysis and reporting.

## Architecture

![Architecture Diagram](https://mermaid.ink/img/pako:eNp1ksFugzAMhl_F8gnUsW5FGhyQetqh0k7bZYceTMGKQqIEqk6r-u5LgDJNmnwK_v3b-W0n0GqJUIJ2te_tQbc8B9_oqvXWw4YMuZo0e90NvZSa48c1ZpGWHD_eL89CbHmMnrqOJDhldW2NdJ1O9nEYWz2SXhQ_gy47EG5JsYDvxqNrZ0kDsZC-HVzgPnlyyj_q_eoUtEQdgHfQIY_SGHtXYZSqz-fLmJ9YC9y__36-XK93hfhaKqVr3RO4Rau-7N_VwvfOI1TBjnYY9GKdvVdTSUd-RTYB8uSdbCZLFXLe_7mZnobRkvagw2Zsk8xLUCON_s8kS6gTiuyuuA0ZkzTJUJU8ozLdp9k2SShLV1MszJZuMaUs326fKI2oRxQwp9uIpQ8FpiRJSJ5nJGPZLs1TzDn_Wz9U2vUw)

The pipeline consists of the following components:

1. **Source Data**: CSV files containing flight booking information
2. **Cloud Storage**: Stores raw input data and PySpark job code
3. **Cloud Composer (Airflow)**: Orchestrates the pipeline workflow
4. **Dataproc Serverless**: Executes PySpark transformation jobs
5. **BigQuery**: Stores processed data for analysis
6. **GitHub Actions**: Automates CI/CD deployment to DEV and PROD environments

## Data Flow

![Data Flow Diagram](https://mermaid.ink/img/pako:eNqNkk1rwzAMhv-K0GmF7ZJjYKUXh8EOZYcdeihasrR4iePZVksp-e-zk5VR1m1shyC9evRIQhdkSIQEXXGr7UHTgkFbTbX1aNFh5oMmqNXZCxXiZoXDXqmM03ZkrVHWKYcDbS3mKBU3qnDeVTkD3Z9PtRb9o33vr2N0Zyqk8_nEZ5hKjVbxg6OkqIQ3a14J_jBQCDfvPx8vq9Um56uiiLr7MpfRJN-Ye1uCM-jM92O5ePTOIpRWjcozP1lnH-1QsogXpAKgF-9kM7RUfkU2HbB5jjfDgRo5ff2Z3jSHEXZjHbSh6aukARUPdnwl8ZxaoMh6yX2IOCdRgqpgCZZxP05WUYJJ_LCNYp5M8AxTki5f-RClEXaIAuY0j1iyVXCGJInJNI1JyuJVMmXMGftrPwG1u44_)

The data flow is as follows:

1. Flight booking CSV data is uploaded to Google Cloud Storage
2. Airflow DAG detects the file and triggers the processing pipeline
3. Dataproc Serverless executes a PySpark job to transform the data
4. Transformed data is loaded into BigQuery tables:
   - Transformed flight data
   - Route insights
   - Origin insights
5. The data is available for analysis and reporting

## Project Structure
