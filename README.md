# AWS Lambda to update RDS from S3 
AWS Lambda function that updates a Postgresql RDS using CSV data from a S3 bucket

## Environment

- S3 bucket contains a CSV file
- RDS Cluster running Postgresql
- AWS Lambda
- Local Ubuntu instance

## Creating your RDS Postgresql DB on AWS

*Login to your AWS Console, select RDS and Create Database*

![](one.PNG)

<hr>

*Choose the Standard Create option and select Amazon Aurora along with PostgreSQL compatibility*

![](two.PNG)

<hr>

*Name your RDS instance and set your username and password*

![](three.PNG)

<hr>

*Important! Set your RDS up for public access and note the VPC Security Group. You will need to adjust this security group to allow incoming traffic to port 5432 from your local Ubuntu Instance*

![](four.PNG)

<hr>

*Under Additional Configuration, create your database name*

![](five.PNG)

<hr>

*Done! Once the databases are up, you can access them using their endpoint name*

![](six.PNG)


## Preparing your local Ubuntu instance

We use a local Ubuntu instance to do the following:
    - To package your Lambda function
    - To connect to remote RDS and create a table

#### Install pre-requisites

```
$sudo apt-get update && install -y python3-pip postgresql-client awscli 
# Copy your AWS client ID and Secret to ~/.aws/credentials
```

#### Setup your RDS table with the required fields

```
$psql -h prod.xxxxxxx.amazonaws.com -U postgres
postgres=> CREATE TABLE Tasks (TaskID serial primary key, VIN varchar(17), HoldNumber varchar(255), Description varchar(255), Location varchar(255), Bay varchar(255), DateTime TIMESTAMPTZ, UserName varchar(255), VehicleScan boolean, VehicleScanLink varchar(255), Issue varchar(255));
postgres=> \d
                List of relations
 Schema |       Name       |   Type   |  Owner
--------+------------------+----------+----------
 public | tasks            | table    | postgres
```

#### Run AWS configure to set your region

AWS configure automatically picks up your keys from ~/.aws/credentials. You just need to set the region when it prompts you to.
For example, we set it here to us-east-1, this is where we had created our RDS database too.

```
$aws configure
Default region name [None]:us-east-1
```




