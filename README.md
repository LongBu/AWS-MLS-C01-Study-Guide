# AWS-MLS-C01-Study-Guide

Note these are my own personal notes and are a work in progress as I study torwards passing this exam.  If this helps someone great, but I make no guarantees/promises.  

## Table of Contents
1. <a href="#introduction">Introduction</a>
2. <a href="#data-engineering">Data Engineering</a>
3. <a href="#exploratory-data-analysis">Exploratory Data Analysis</a>
4. <a href="#modeling">Modeling</a>
5. <a href="#machine-learning-implementation-and-operations">Machine Learning Implementation and Operations</a>
6. <a href="#acronyms">Acronyms</a>

## Introduction
<a href="https://d1.awsstatic.com/training-and-certification/docs-sa-pro/AWS-Certified-Solutions-Architect-Professional_Exam-Guide.pdf">AWS Certified Machine Learning – Specialty (MLS-C01) Exam Guide</a>
### Exam Content Breakdown:

| Domain  | % of Exam |
| ------------- | ------------- |
| Domain 1: Data Engineering | 20%  |
| Domain 2: Exploratory Data Analysis | 24%  |
| Domain 3: Modeling | 36% |
| Machine Learning Implementation and Operations | 20% |
| **Total** | **100%** |

## Data Engineering 

### Create data repositories for machine learning
  * Identify data sources (e.g., content and location, primary sources such as user data)
		* Determine storage mediums (e.g., DB, Data Lake, S3, EFS, EBS) 
### Identify and implement a data ingestion solution.
  * Data job styles/types (batch load, streaming)
  * Data ingestion pipelines (Batch-based ML workloads and streaming-based ML workloads)
    * Kinesis
    * Kinesis Data Analytics
    * Kinesis Firehose
    * EMR
    * AWS Glue 
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
  * Job scheduling 
### Identify and implement a data transformation solution. 
  * Handle ML-specific data using map reduce (Hadoop, Spark, Hive) 
  * Transforming data transit (ETL: Glue, EMR, AWS Batch)
#### AWS Batch:
  * Fully managed batch processing at any scale using dynamically launched *EC2 instances (spot)*
  * Job with a start and an end (not continuous)
  * Can run 100,000s of computing batch jobs
  * You submit/schedule batch jobs and AWS Batch handles it
  * Provisions right amount of compute/memory
  * Batch jobs are defined as *docker images and run on ECS*
  * Helpful for cost optimization and focusing less on infrastructure
  * No time limit
  * Any run time packaged in docker image
  * Rely on EBS/instance store for disk space
  * Advantage over λ=>time limit, limited runtimes, limited disk space

## Exploratory Data Analysis



### Sanitize and prepare data for modeling
  * Identify and handle missing data, corrupt data, stop words, etc.
  * Formatting, normalizing, augmenting, and scaling data
  * Labeled data (recognizing when you have enough labeled data and identifying mitigation
  * strategies [Data labeling tools (Mechanical Turk, manual labor)])
### Perform feature engineering
  * Identify and extract features from data sets, including from data sources such as text, speech,image, public datasets, etc.
  * Analyze/evaluate feature engineering concepts (binning, tokenization, outliers, synthetic features, 1 hot encoding, reducing dimensionality of data)
### Analyze and visualize data for machine learning
  * Graphing (scatter plot, time series, histogram, box plot)
  * Interpreting descriptive statistics (correlation, summary statistics, p value)
  * Clustering (hierarchical, diagnosing, elbow plot, cluster size)
#### Amazon Athena:
  * Serverless query service enabling analysis and querying of data in S3 using standard SQL, while allowing more advanced queries (joins permitted)
  * Compress data for smaller retrieval
  * Use target files (> 128 MB) to minimize overhead
  * $5.00 per TB scanned
  * Commonly used with Amazon Quicksight
  * Federated query allows SQL queries across relational, object, non-relational, custom (AWS or on-premisis) using Data Source Connectors that run on λ with results being returned and stored in S3

## Modeling
### Frame business problems as machine learning problems. 
  * Determine when to use/when not to use ML
  * Know the difference between supervised and unsupervised learning
  * Selecting from among classification, regression, forecasting, clustering, recommendation, etc.
### Select the appropriate model(s) for a given machine learning problem
  * Xgboost, logistic regression, K-means, linear regression, decision trees, random forests, RNN, CNN, Ensemble, Transfer learning
  * Express intuition behind models
### Train machine learning models
  * Train validation test split, cross-validation
  * Optimizer, gradient descent, loss functions, local minima, convergence, batches, probability, etc. 
  * Compute choice (GPU vs. CPU, distributed vs. non-distributed, platform [Spark vs. non-Spark])
  * Model updates and retraining
     * Batch vs. real-time/online 
### Perform hyperparameter optimization. 
  * Regularization
    * Drop out
    * L1/L2 
  * Cross validation
  * Model initialization
  * Neural network architecture (layers/nodes), learning rate, activation functions
  * Tree-based models (# of trees, # of levels)
  * Linear models (learning rate)
### Evaluate machine learning models.
  * Avoid overfitting/underfitting (detect and handle bias and variance)
  * Metrics (AUC-ROC, accuracy, precision, recall, RMSE, F1 score)
  * Confusion Matrix:
    * Recall = TP/(TP + FN)
    * Precision = TP/(TP + FP)
    * Accuracy = (TP + TN)/(TP + FP + TN + FN)
    * F1 Score (harmonic mean of precision and recall) = TP/(TP + (FN + FP/2))
  * Offline and online model evaluation, A/B testing
  * Compare models using metrics (time to train a model, quality of model, engineering costs)
  * Cross validation 

## Machine Learning Implementation and Operations

### Build machine learning solutions for performance, availability, scalability, resiliency, and fault tolerance. 
  * AWS environment logging and monitoring
    * CloudTrail and CloudWatch
    * Build error monitoring 
  * Multiple regions, Multiple AZs
  * AMI/golden image
  * Docker containers
  * Auto Scaling groups
  * Rightsizing
    * Instances
    * Provisioned IOPS
    * Volumes
  * Load balancing
  * AWS best practices
### Recommend and implement the appropriate machine learning services and features for a given problem.
  * ML on AWS (application services)
    * Poly
    * Lex
    * Transcribe
  * AWS service limits
  * Build your own model vs. SageMaker built-in algorithms
  * AWS SageMaker
    * File Mode
    * Pipe Mode
  * Infrastructure: (spot, instance types), cost considerations
    * Using spot instances to train deep learning models using AWS Batch 
### Apply basic AWS security practices to machine learning solutions. 
  * IAM
  * S3 bucket policies
  * Security groups
  * VPC
  * Encryption/anonymization
### Deploy and operationalize machine learning solutions.
  * Exposing endpoints and interacting with them
  * ML model versioning
  * A/B testing
  * Retrain pipelines
  * ML debugging/troubleshooting
    * Detect and mitigate drop in performance
    * Monitor performance of the model 


## Acronyms

| Acronym  | Definition |
| ------------- | ------------- |
| EMR | Elastic Map Reduce |
| ETL | Extract, Translate, Load |
| FN | False Negative |
| FP | False Positive |
| TN | True Negative |
| TP | True Positive |
