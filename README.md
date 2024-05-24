# Spotify-ETL-Pipeline
This project implements an ETL (Extract, Transform, Load) pipeline using AWS services to process data from the Spotify API. The pipeline extracts data from Spotify, transforms it into a structured format, and loads it into Amazon S3 for further analysis using AWS Glue and Amazon Athena.

Project Overview
Architecture

    Extract:
        Spotify API: Source of raw data.
        AWS Lambda (Data Extraction): A Lambda function extracts data from the Spotify API and stores it in an S3 bucket.
        Amazon S3 (Raw Data): The bucket where raw data is stored.
        Amazon CloudWatch (Daily Trigger): A CloudWatch rule triggers the data extraction Lambda function daily.

    Transform:
        AWS Lambda (Data Transformation): A Lambda function processes and transforms the raw data.
        Amazon S3 (Transformed Data): The bucket where transformed data is stored.

    Load:
        AWS Glue Crawler: A service to infer the schema of the transformed data and create tables in the AWS Glue Data Catalog.
        AWS Glue Data Catalog: A central metadata repository that stores schema and table definitions.
        Amazon Athena: A query service that analyzes the transformed data stored in S3 using standard SQL.

Workflow

    Data Extraction:
        A CloudWatch rule triggers the data extraction Lambda function every minute.
        The Lambda function retrieves playlist data from the Spotify API and stores it in the raw_data/to_processed/ folder in S3.

    Data Transformation:
        An S3 event triggers the data transformation Lambda function whenever a new file is uploaded to the raw_data/to_processed/ folder.
        The Lambda function processes the raw data, transforming it into CSV format, and stores the results in the appropriate folders in S3.
        The processed raw data files are moved to the raw_data/processed/ folder to avoid reprocessing.

    Data Loading:
        An AWS Glue Crawler runs on a schedule to infer the schema of the transformed data and update the AWS Glue Data Catalog.
        Amazon Athena is used to query and analyze the transformed data.

Prerequisites

    AWS Account
    Spotify Developer Account
    Python 3.8+
    AWS CLI configured
