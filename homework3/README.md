### Solutions for week 3
-- CREATING SCHEMA FOR YELLOW TAXI DATA  
CREATE SCHEMA IF NOT EXISTS `dezc-dw-hw3.taxidata`
OPTIONS (
  location = 'us-west3'
);

-- CREATING EXTERNAL TABLE FOR THE PARQUET FILES IN THE BUCKET  
CREATE OR REPLACE EXTERNAL TABLE `dezc-dw-hw3.taxidata.yellow_taxi_external`
OPTIONS (
  format = 'PARQUET',
  uris = ['gs://sm_dezoomcamp_hw3/*.parquet']
);

-- CREATING REGULAR TABLE  
CREATE OR REPLACE TABLE `dezc-dw-hw3.taxidata.yellow_taxi_data`
AS
SELECT * FROM `dezc-dw-hw3.taxidata.yellow_taxi_external`;

-- Q1 - Count of records  
SELECT COUNT(*) FROM `dezc-dw-hw3.taxidata.yellow_taxi_external`; --20332093

-- Q2 - Data read estimation  
SELECT COUNT(DISTINCT PULocationID) FROM `dezc-dw-hw3.taxidata.yellow_taxi_external`; --0 MB
SELECT COUNT(DISTINCT PULocationID) FROM `dezc-dw-hw3.taxidata.yellow_taxi_data`; --155.12 MB

-- Q3 - Understanding columnar storage  
SELECT DISTINCT PULocationID FROM `dezc-dw-hw3.taxidata.yellow_taxi_data`;
SELECT DISTINCT PULocationID, DOLocationID FROM `dezc-dw-hw3.taxidata.yellow_taxi_data`;
-- BigQuery is a columnar database, and it only scans the specific columns requested in the query. Querying two columns (PULocationID, DOLocationID) requires reading more data than querying one column (PULocationID), leading to a higher estimated number of bytes processed.

-- Q4 - Counting zero fare trips  
SELECT COUNT(*) FROM `dezc-dw-hw3.taxidata.yellow_taxi_data` WHERE fare_amount = 0; --8333

-- Q5 - Partitioning and clustering  
-- The best strategy to make an optimized table in Big Query if your query will always filter based on tpep_dropoff_datetime and order the results by VendorID is to - Partition by tpep_dropoff_datetime and Cluster on VendorID
CREATE OR REPLACE TABLE `dezc-dw-hw3.taxidata.yellow_taxi_data_optimized`
PARTITION BY DATE(tpep_dropoff_datetime)
CLUSTER BY VendorID
AS
SELECT *
FROM `dezc-dw-hw3.taxidata.yellow_taxi_data`;

-- Q6 - Partition benefits  
SELECT DISTINCT VendorID FROM `dezc-dw-hw3.taxidata.yellow_taxi_data`
WHERE tpep_dropoff_datetime >= '2024-03-01' AND tpep_dropoff_datetime < '2024-03-16'; --310.24 MB
SELECT DISTINCT VendorID FROM `dezc-dw-hw3.taxidata.yellow_taxi_data_optimized`
WHERE tpep_dropoff_datetime >= '2024-03-01' AND tpep_dropoff_datetime < '2024-03-16'; --26.84 MB

-- Q7 - External table storage  
-- Where is the data stored in the External Table you created? GCP Bucket

-- Q8 - Clustering best practices  
-- It is best practice in Big Query to always cluster your data: False. Only useful if we group by or order or filter those columns. Also not useful if size is small

-- Q9 - Understanding table scans  
SELECT COUNT(*) FROM `dezc-dw-hw3.taxidata.yellow_taxi_data`; --0 B scanned as BQ can get this info from the metadata 

