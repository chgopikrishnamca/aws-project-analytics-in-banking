
# Banking Analytics: AWS Capstone Project

WIP.

This project involves in building a Banking Analytics Lakehouse that processes daily transaction files and stores them in Amazon S3 Tables—a purpose-built storage tier for Apache Iceberg that provides high-performance transactional consistency. 

### Project Goal

To build a scalable, automated, analytics-ready data pipeline using AWS services, enabling meaningful insights from banking data.

### Technology Stack

1. Amazon S3 - Data lakes (raw, staging, optimized zones)
2. AWS Glue Studio Note books - To write pyspark scripts
3. AWS Glue Crawler - Schema inference & Data Catalog population
4. AWS Glue Catalog - Populate catalog information
5. AWS Lambda - Trigger ETL jobs
6. Amazon Athena - Serverless querying
7. Amazon Event Bridge - To Schedule Glue ETL jobs
8. Amazon SNS - To setup email notifications

Languages & Tools : Python, PySpark, SQL

### Dataset Details

Raw CSV files and their fields:

1. customers.csv: customer_id, name, email, country
2. accounts.csv: account_id, customer_id, account_type (Savings/Current), balance.
3. transactions.csv:  txn_id, account_id, amount, txn_type (Credit/Debit), timestamp. 

#### Data Lake Structure - S3 Folder Structure
1. Raw Data (Landing Area) : s3://banking-app-landing-area/

    s3://banking-app-landing-area/customers/

    s3://banking-app-landing-area/accounts/

    s3://banking-app-landing-area/transactions/

2. Optimized Data (Gold Layer) : s3://banking-app-processed-data/

### Pipeline Steps
#### Step 1 : Create S3 buckets.

- Raw Data: s3://banking-app-landing-area/
- Processed Data: s3://banking-app-processed-data/

#### Step 2 : Upload Raw CSV Files into respective folders. 

- s3://banking-app-landing-area/customers/
- s3://banking-app-landing-area/accounts/
- s3://banking-app-landing-area/transactions/

Once files are uploaded, please add "_DONE.txt" file to to "s3://ecom-app-landing-area/"  trigger ETL1 job.

#### Step3: Create IAM Roles 

1. Role: AWSGlueETLRole-BankApp 

- S3 read/write for landing + staging + optimized 
- CloudWatch Logs 

2. Role: LambdaExecutionRole-BankApp 

- S3 Read 
- Glue:StartJobRun 
- CloudWatch Logs 

#### Step 4: Create Glue Crawlers

1. crawl-raw-data-job : crawls raw data from s3://ecom-app-landing-area
2. crawl-processed-data-job : crawls staging data from s3://ecom-app-processed-data/staging/

#### Step 5 : Create Glue jobs for Data Cleaning & Transformations

1. ETL Job: ETL Job - Transform Raw Data : Involves in data cleaning.

✔ Schema Enforcement

- Casting datatypes
- Converting string→date, bigint→int, double, etc.

✔ Data Cleaning

- Handling nulls
- Imputing missing values (like default country = "India")
- Removing duplicates
- Trimming text fields

✔ Output

Cleaned Parquet files → Stored in staging area bucket.

#### Step 6 : Create Automation Triggers 

- lambda-etl1-trigger-job : Triggers ETL job1
- lambda-etl2-trigger-job-daily : Triggers ETL2 job
- Amazon Event Bridge Scheduler : Invokes lambda function "lambda-etl2-trigger-job-daily"

#### Step 5 : Query Athena Tables

Crawlers scan the optimized S3 folders and generate analytics-ready tables:


#### Athena Analytics Queries



### Key Insights Derived




### Challenges & Solutions



### Future Enhancements

