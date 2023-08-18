# Udacity-NDDE-Final Project - Data Pipelines with Airflow

This project is part of Udacity Data Engineer Nanodegree. 

In this project, I applied what I have learned on data pipelines using Apache Airflow and AWS Redshift. To complete the project, I created  custom operators to perform tasks such as staging the data, filling the data warehouse, and running checks on the data as the final step.

## Project Overview
A music streaming company, Sparkify, has decided that it is time to introduce more automation and monitoring to their data warehouse ETL pipelines and come to the conclusion that the best tool to achieve this is Apache Airflow.

The project involved creating high grade data pipelines that are dynamic and built from reusable tasks, can be monitored, and allow easy backfills. The data quality plays a big part when analyses are executed on top the data warehouse and want to run tests against their datasets after the ETL steps have been executed to catch any discrepancies in the datasets.

The source data resides in S3 and needs to be processed in Sparkify's data warehouse in Amazon Redshift. The source datasets consist of JSON logs that tell about user activity in the application and JSON metadata about the songs the users listen to.

## DAG

The following dag was completed:

![Dag](dag.png)


## Staging the data

The data were staged from S3 to Redshift.
The airflow tasks uses parameters to generate the copy statement dynamically.
The operator contains logging in different steps of the execution.
The SQL statements are executed by using a Airflow hook.

## Loading dimensions and facts

	
Dimensions are loaded with on the LoadDimension operator.
Facts are loaded with on the LoadFact operator.
Instead of running a static SQL statement to stage the data, the task uses params to generate the copy statement dynamically.
The DAG allows to switch between append-only and delete-load functionality.

## Data Quality Checks

Data quality check is done with correct operator.
The DAG either fails or retries n times.
Operator uses params to get the tests and the results, tests are not hard coded to the operator.