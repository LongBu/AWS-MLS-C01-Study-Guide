# AWS-MLS-C01-Study-Guide

Note these are my own personal notes and are a work in progress as I study torwards passing this exam.  If this helps someone great, but I make no guarantees/promises.  

## Data Engineering 
### AWS Glue
  * Managed ETL service (fully serverless) used to prepare/transform data for analysis
  * Can be event driven (eg: λ triggered by S3 put object) to call Glue ETL
  * Glue Data catalog uses an AWS Glue Data Crawler scanning DBs/S3/data to write associated metadata utilized by Glue ETL, or data discovery on Athena, Redshift Spectrum or EMR
  * Glue Job bookmarks prevent reprocessing old data
  * Glue Databrew-clean/normalize data using pre-built transformation
  * Glue Studio-new GUI to create, run, and monitor ETL jobs in Glue
  * Glue Streaming ETL (built on Apache Spark Structured Streaming)-compatible with Kinesis Data Streaming, Kafka, MSK
  * Glue Elastic Views:
    * Combine and replicate data across multiple data stores using SQL (View)
    * No custom code, Glue monitors for changes in the source data, serverless
    * Leverages a "virtual table" (materialized view)
## Exploratory Data Analysis 
## Modeling 
### Confusion Matrix
  * Recall = TP/(TP + FN)
  * Precision = TP/(TP + FP)
  * Accuracy = (TP + TN)/(TP + FP + TN + FN)
  * F1 Score (harmonic mean of precision and recall) = TP/(TP + (FN + FP/2))
## Machine Learning Implementation and Operations

## Acronyms

| Acronym  | Definition |
| ------------- | ------------- |
| EMR | Elastic Map Reduce |
| ETL | Extract, Translate, Load |
| FN | False Negative |
| FP | False Positive |
| TN | True Negative |
| TP | True Positive |
