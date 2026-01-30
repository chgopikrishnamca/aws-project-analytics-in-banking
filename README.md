
# Banking Analytics: AWS Capstone Project

This project involves in building a Banking Analytics Lakehouse that processes daily transaction files and stores them in Amazon S3 Tables—a purpose-built storage tier for Apache Iceberg that provides high-performance transactional consistency. 

### Project Goal

To build a scalable, automated, analytics-ready data pipeline using AWS services, enabling meaningful insights from banking data.

### Technology Stack

1. Amazon S3 - Data lakes, Iceberg Table data
2. AWS Glue Script - To write pyspark scripts
3. Iceberg - To have optmized/enrichied data in iceberg tables.
4. Amazon Athena - To query enriched data
5. Amazon SNS - To setup email notifications

Languages & Tools : Python, PySpark, SQL

### Dataset Details

Usually we can collect datasets from any source like kaggle. Here we have generated datasets for practice purpose using a python script located in "/Python Snippets/generaye_datasets.py". This script generates files as below.

1. customers.csv: customer_id, name, email, country
2. accounts.csv: account_id, customer_id, account_type (Savings/Current), balance.
3. transactions.csv:  txn_id, account_id, amount, txn_type (Credit/Debit), timestamp. 

Put these files in to s3://banking-app-landing-area/raw.

#### Data Lake Structure - S3 Folder Structure
1. Raw Data (Landing Area) : s3://banking-app-landing-area/raw/

    s3://banking-app-landing-area/raw/customers/

    s3://banking-app-landing-area/raw/accounts/

    s3://banking-app-landing-area/raw/transactions/

2. Optimized Data (Gold Layer) : s3://banking-app-processed-data/

### Pipeline Steps
#### Step 1 : Create S3 buckets.

- Raw Data: s3://banking-app-landing-area/
- Enriched Iceberg Warehouse Data: s3://bank-app-lakehouse-iceberg/

#### Step 2 : Upload Raw CSV Files into respective folders. 

- s3://banking-app-landing-area/customers/
- s3://banking-app-landing-area/accounts/
- s3://banking-app-landing-area/transactions/

Schedule the job to run on specific time using Amazon scheduler or run on demand daily basis. 

#### Step3: Create IAM Roles 

1. Role: AWSGlueServiceRole-BankAppAnalytics

- S3 read/write permissions
- CloudWatch Logs permissions

#### Step 4 : Create Glue jobs for Data Cleaning & Transformations

1. ETL Job: ETLBankAppAnalytics : AWS Glue Job that involves in transforming and writing enriched data to iceberf g tables.


#### Step 5 : Create Automation Triggers (optional, we are running this on demand on daily basis)

1. create a lambda function that triggers AWS Glue ETL job.
2. Use Amazon Event Bridge Scheduler torun Lamda Function on daily basis.

#### Step 5 : Query Athena Tables

Glue job writes the enriched data to Iceberf tables, which can be queried through athena.


#### Athena Analytics Queries
Please look into the PPT file for queries

### Key Insights Derived
Customer Behaviour
Bank Performance
Bank Audit Purposes
Fraud Detection

### Future Enhancements
1. ETL job Can be automated using a lambda function.
2. Data Sets can be more realistic by taking from kaggle or any other site.
3. Can implement Event based processing as well, based on the requirement.
