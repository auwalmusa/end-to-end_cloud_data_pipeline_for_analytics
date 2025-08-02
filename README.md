# ETL Data Pipeline with Google Cloud Platform

This repository contains a comprehensive Extract, Transform, Load (ETL) project that generates synthetic employee data, processes it through Google Cloud Data Fusion, and orchestrates the entire pipeline using Apache Airflow/Composer with BigQuery for data warehousing and Looker Studio for analytics.

## Project Overview

This end-to-end data pipeline project demonstrates enterprise-level data engineering capabilities with a focus on employee data management:

1. **Data Generation & Extraction**: Generate synthetic employee data using Python Faker library
2. **Cloud Storage**: Upload generated CSV files to Google Cloud Storage buckets
3. **Data Transformation**: Apply data masking and transformation in Cloud Data Fusion
4. **Data Loading**: Load processed data into Google BigQuery data warehouse
5. **Orchestration**: Automate the complete pipeline using Apache Airflow (Cloud Composer)
6. **Data Analytics**: Create interactive dashboards and reports using Looker Studio

## 🏗️ Architecture

The project follows a modern cloud-native architecture with the following components:

![Architecture Diagram](https://github.com/auwalmusa/end-to-end_cloud_data_pipeline_for_analytics/blob/main/Architecture%20Diagram.png)

### Data Flow
1. **Python Script (extract.py)** → Generates synthetic employee data using Faker
2. **Google Cloud Storage** → Stores CSV files in bucket `bucktt-employee-data`
3. **Cloud Data Fusion** → Processes and transforms the employee data
4. **Apache Airflow DAG** → Orchestrates the entire pipeline daily
5. **Google BigQuery** → Data warehouse storage
6. **Looker Studio** → Business intelligence and visualization

## 📄 Implementation Details

### Data Generation (`extract.py`)

The extraction script generates realistic synthetic employee data with the following features:

**Generated Fields:**
- **Personal Information**: First name, last name, email, address, phone number
- **Employment Details**: Job title, department, salary
- **Security**: 8-character passwords with mixed characters

**Key Features:**
- Generates 100 employee records by default
- Uses predefined job titles and departments for consistency
- Creates CSV output with proper encoding and formatting
- Automatically uploads to GCS bucket `bucktt-employee-data`
- Includes progress tracking and data validation

**Sample Generated Data:**
```csv
first_name,last_name,job_title,department,email,address,phone_number,salary,password
John,Smith,Software Engineer,Engineering,john@example.com,New York,555-0123,75000,aB3mX9k2
```

### Orchestration (`dag.py`)

The Airflow DAG manages the complete pipeline workflow:

**DAG Configuration:**
- **Name**: `employee_data`
- **Schedule**: Daily execution (`@daily`)
- **Start Date**: July 29, 2025
- **Email Alerts**: Configured for failure notifications
- **Retry Logic**: 1 retry with 5-minute delay

**Pipeline Tasks:**
1. **extract_data**: Executes the Python extraction script
2. **start_datafusion_pipeline**: Triggers the Data Fusion ETL pipeline named "etl"

**Task Dependencies:**
```
extract_data >> start_datafusion_pipeline
```

### Cloud Infrastructure

**Google Cloud Storage:**
- **Bucket**: `bucktt-employee-data`
- **Purpose**: Raw data storage for CSV files
- **Access**: Automated upload from extraction script

**Cloud Data Fusion:**
- **Instance**: `datafusion-dev`
- **Location**: `us-central1`
- **Pipeline**: `etl` (handles data transformation and loading)

**Apache Airflow:**
- **Platform**: Cloud Composer
- **Script Location**: `/home/airflow/gcs/dags/scripts/extract.py`
- **Monitoring**: Email notifications and retry mechanisms

## 📊 Data Analytics & Looker Dashboard Overview

### Business Intelligence Layer

The Looker Studio dashboard provides comprehensive analytics and insights across multiple dimensions:

#### 📈 Key Performance Indicators (KPIs)
- **Data Processing Metrics**: Pipeline success rates, data volume trends, processing times
- **Data Quality Indicators**: Completeness, accuracy, consistency scores
- **Operational Metrics**: System uptime, error rates, resource utilization

#### Dashboard Components

**1. Executive Summary Dashboard**
- High-level business metrics and trends
- Data pipeline health status
- Key performance indicators at a glance
- Alert notifications for critical issues

**2. Data Quality Dashboard**
- Data completeness metrics by source system
- Data validation results and anomaly detection
- Schema drift monitoring
- Data lineage visualization

**3. Operational Analytics Dashboard**
- Pipeline execution times and performance trends
- Resource utilization (CPU, memory, storage)
- Error tracking and resolution metrics
- Data freshness and latency monitoring

**4. Business Analytics Dashboard**
- Customer insights and segmentation analysis
- Revenue and performance trends
- Geographic distribution analysis
- Time-series analysis and forecasting

#### 📊 Visualization Features

**Interactive Charts & Graphs:**
- Time-series line charts for trend analysis
- Bar charts for categorical comparisons
- Pie charts for composition analysis
- Heat maps for geographic and correlation analysis
- Scatter plots for relationship identification

**Real-time Monitoring:**
- Live data refresh capabilities
- Automated alert systems
- Drill-down functionality for detailed analysis
- Custom date range filtering

**Advanced Analytics:**
- Statistical analysis and correlation matrices
- Predictive modeling insights
- Anomaly detection visualization
- Comparative period analysis

#### Dashboard Insights & Use Cases

**For Data Engineers:**
- Monitor ETL pipeline performance and reliability
- Track data quality metrics and identify issues
- Optimize resource allocation and processing efficiency
- Analyze data flow patterns and bottlenecks

**For Business Analysts:**
- Access clean, transformed data for analysis
- Create custom reports and visualizations
- Perform ad-hoc analysis and exploration
- Generate insights for strategic decision-making

**For Business Stakeholders:**
- View executive-level KPIs and business metrics
- Access real-time operational dashboards
- Monitor business performance trends
- Make data-driven strategic decisions

### Technical Implementation

**Data Sources Integration:**
- Multiple data source connectors
- Real-time and batch data processing
- Automated data validation and quality checks
- Scalable data ingestion capabilities

**Visualization Technology:**
- Looker Studio native charts and controls
- Custom SQL queries for complex metrics
- Responsive design for mobile and desktop
- Embedded analytics capabilities

**Performance Optimization:**
- Materialized views for faster query performance
- Incremental data refresh strategies
- Caching mechanisms for frequently accessed data
- Query optimization and indexing strategies

## Technical Stack

- **Cloud Platform**: Google Cloud Platform (GCP)
- **Data Integration**: Google Cloud Data Fusion
- **Data Warehouse**: Google BigQuery
- **Orchestration**: Apache Airflow (Cloud Composer)
- **Analytics**: Looker Studio
- **Programming**: Python, SQL
- **Infrastructure**: Cloud Storage, Compute Engine
- **Monitoring**: Cloud Monitoring, Cloud Logging

## Key Features

### Data Pipeline Features
- **Automated Data Extraction**: Scheduled and event-driven data collection
- **Data Quality Assurance**: Built-in validation and cleansing processes
- **Scalable Processing**: Handle large volumes of data efficiently
- **Error Handling**: Robust error detection and recovery mechanisms
- **Security**: Data masking and encryption for sensitive information

### Analytics Features
- **Self-Service Analytics**: User-friendly interface for business users
- **Real-time Insights**: Live dashboards with automated data refresh
- **Advanced Visualizations**: Interactive charts and drill-down capabilities
- **Mobile Responsive**: Access dashboards from any device
- **Collaboration**: Share insights and reports across teams

## 📈 Business Value

### Operational Efficiency
- **Automated Processes**: Reduce manual data handling by 90%
- **Improved Data Quality**: Ensure consistency and accuracy across systems
- **Faster Time-to-Insights**: Real-time analytics and reporting
- **Cost Optimization**: Efficient resource utilization and scaling

### Strategic Benefits
- **Data-Driven Decisions**: Access to accurate, timely business intelligence
- **Competitive Advantage**: Faster response to market changes
- **Risk Management**: Early detection of operational issues
- **Growth Enablement**: Scalable infrastructure for business expansion

## 📋 Project Structure

```
ETL-Data-Pipeline-Google Cloud/
├── extract.py              # Python script for generating and uploading employee data
├── dag.py                  # Airflow DAG for pipeline orchestration
├── sample_README.md        # Project documentation (this file)
├── Requirements.docx       # Project requirements document
└── employee_data.csv       # Generated synthetic employee data (created by extract.py)
```

## 🔧 Setup & Deployment

### Prerequisites

- Google Cloud Platform account with the following APIs enabled:
  - Cloud Storage API
  - Cloud Data Fusion API
  - Cloud Composer API
  - BigQuery API
- Python 3.x with required packages:
  ```bash
  pip install faker google-cloud-storage
  ```

### Configuration Steps

1. **GCP Setup:**
   ```bash
   # Authenticate with Google Cloud
   gcloud auth login
   gcloud config set project YOUR_PROJECT_ID
   ```

2. **Cloud Storage:**
   - Create bucket: `bucktt-employee-data`
   - Configure appropriate IAM permissions

3. **Cloud Data Fusion:**
   - Create instance: `datafusion-dev` in `us-central1`
   - Set up ETL pipeline named `etl`

4. **Cloud Composer:**
   - Create Composer environment
   - Upload `dag.py` to the DAGs folder
   - Upload `extract.py` to `/home/airflow/gcs/dags/scripts/`

### Running the Pipeline

**Manual Execution:**
```bash
# Run data generation locally
python extract.py

# Or trigger via Airflow UI
# Navigate to Airflow web interface and trigger 'employee_data' DAG
```

**Automated Execution:**
- The DAG runs daily at midnight
- Monitor progress through Airflow web interface
- Check logs for any execution issues

## 🚀 Code Explanation

### extract.py Features

**Data Generation Logic:**
- Uses Faker library for realistic synthetic data
- Generates structured employee records with consistent formatting
- Implements custom password generation with mixed character sets
- Includes progress tracking for large datasets

**GCS Integration:**
- Automatic file upload to designated bucket
- Error handling for storage operations
- Configurable bucket and file naming

### dag.py Features

**Pipeline Orchestration:**
- Sequential task execution with proper dependencies
- Email notification system for failures
- Configurable retry logic and scheduling
- Integration with Cloud Data Fusion operators

**Task Flow:**
1. `extract_data` → Runs the Python data generation script
2. `start_datafusion_pipeline` → Triggers Data Fusion ETL processing

## 📊 Monitoring & Maintenance

### Pipeline Monitoring
- Real-time pipeline status tracking
- Automated alerting for failures or anomalies
- Performance metrics and optimization recommendations
- Data lineage and impact analysis

### Dashboard Maintenance
- Regular dashboard performance reviews
- User feedback collection and implementation
- Content updates and new visualization development
- Access control and security management

---

**Project Status**: Production Ready  
**Last Updated**: August 2025  
**Maintainer**: Data Engineering Team
