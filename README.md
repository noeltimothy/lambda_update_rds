# AWS Lambda to update RDS from S3 
AWS Lambda function that updates a Postgresql RDS using CSV data from a S3 bucket

## Environment

- S3 bucket contains a CSV file
- RDS Cluster running Postgresql
- AWS Lambda
- Local Ubuntu instance

## Creating your RDS Postgresql DB on AWS

__STEP 1__

Login to your AWS Console, select RDS and Create Database
![]('one.png')

__STEP 2__

![](./two.png)

## Preparing your local Ubuntu instance

We use a lical Ubuntu instance to do the following:
    - To package your Lambda function
    - To connect to remote RDS and create a table

### 
