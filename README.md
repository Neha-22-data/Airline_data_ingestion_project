# Airline-Data-Ingestion-Project
***
## Project Overview
This project is an overview of an Event Driven Sales Data Projection data pipeline that Process the Orders data based on their Status and route towards DynamoDB or SQS as per the Business requirement rules.
An airline daily data ingestion project using S3, S3 Cloudtrail Notification, Event Bridge Pattern Rule, Glue Crawler, Glue Visual ETL, SNS, Redshift, and Step Function

***

## Architectural Diagram
![AirlineProject](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/AirlineProject.jpg)

***

## Key Steps
### 1. Create a S3 bucket
- we will create a S3 bucket "airline-data-input" to store the airport dimension file and daily input files.
[images/S3.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/S3.JPG)

### 2. Create a Schema in Redshift
- we will create a "airlines" schema in Redshift with both the Tables.
    - airport_dim
    - daily_flights_fact
[images/Redshift.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/Redshift.JPG)

- Copy the aiports data from S3 to Reshift aiport_dim table.
[https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/Redshift.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/Redshift.JPG)


### 3. Create Glue Crawlers for Redshift Tables
- we will create glue crawlers for the Redshift tables.
  [images/RedShift_Crawlers.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/RedShift_Crawlers.JPG)


### 4. Create Glue Crawlers for S3 Input data
- first we will create a dummy hive style folder in our S3 and upload a dummy data file to create the crawler.
- S3 Data Input File
  [images/S3-flihgt-data.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/S3-flihgt-data.JPG)
  
- S3 Glue Crawler
  [images/S3-crawler.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/S3-crawler.JPG)
  
- Glue Tables
  [images/glue-tables.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/glue-tables.JPG)


### 5. Create Glue ETL Pipeline
- we will create a Glue Pipeline "flight-data-ingestion-pipeline" in which we join our daily data with the airport-dim and create a denormalized table for further analysis.
[images/glue-pipeline.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/glue-pipeline.JPG)

### 6. Create SNS
- we will create a SNS Topic "glue-job-notification" and subscribed by your email address to get the notification.
[images/SNS.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/SNS.JPG)

### 7. Create State Machine using Step Function
- we will create a State Machine using Step Function service and create a complete workflow in it. 
[images/StateMachine.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/StateMachineSuccess.JPG)

### 8. Create an Event Rule
- we will create an Event Rule "Airline-S3-StepFunc-EventRule" Which will triger the State Machine on a Object Creation in airline data S3 bucket.
 [images/EventRule.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/EventRule.JPG)


### 9. Create an Event Bridge Rule
- we will create an Event Rule "Airline-S3-StepFunc-EventRule" Which will triger the State Machine on a Object Creation in airline data S3 bucket.
[images/EventRule.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/EventRule.JPG)

### 9. Upload the input flight data csv file 
- we will upload the input flight data csv file in the input S3 bucket which will trigger the State machine using Event Bridge Rule.
- S3 file
[images/fileUpload.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/fileUpload.JPG)
- Glue Job Run
[images/glueJobRun.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/glueJobRun.JPG)
- State Machine Run
[images/StateMachineSuccess.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/StateMachineSuccess.JPG)

### 9. Output
- we can see the Success Notification in your subscribed mail box 
[images/mailNoti.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/mailNoti.JPG)

- we can the output data stored in Redshift fact table.
[images/factData.JPG](https://github.com/Neha-22-data/Airline_data_ingestion_project/blob/main/images/factData.JPG)
